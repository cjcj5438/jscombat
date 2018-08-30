# username

# 简单介绍 #
用于获取当前用户名

# 用法 #

支持异步和promise异步写法:
```javascript
const username = require('username');

// 同步
console.log(username.sync()); // => 'elvin'

// 异步
username().then(username => {
    console.log(username); // => 'elvin'
});


```

# 源码学习 #

> 主要逻辑:
1. 首先通过 process.env 变量中的值获得用户名，若存在，直接返回；
2. 接着若存在 os.userinfo 函数，则通过 os.userinfo().username 获得用户名并返回；
3. 若上述方法均失败，则在 OS X/Linux 下通过执行 id -un 命令，Windows 下通过 whoami 命令获得用户名并返回。



```javascript
'use strict';
const os = require('os');
const execa = require('execa');
const mem = require('mem');

const getEnvVar = () => {
	const {env} = process;

	return env.SUDO_USER ||
		env.C9_USER /* Cloud9 */ ||
		env.LOGNAME ||
		env.USER ||
		env.LNAME ||
		env.USERNAME;
};

const cleanWinCmd = x => x.replace(/^.*\\/, '');

const noop = () => {};

module.exports = mem(() => {
	const envVar = getEnvVar();

	if (envVar) {
		return Promise.resolve(envVar);
	}
	// 源码中从 process.env 无法获取用户名时，会尝试通过 os.userInfo() 函数获取
	if (os.userInfo) {
		return Promise.resolve(os.userInfo().username);
	}

	if (process.platform === 'win32') {
		return execa('whoami').then(x => cleanWinCmd(x.stdout)).catch(noop);
	}

	return execa('id', ['-un']).then(x => x.stdout).catch(noop);
});

module.exports.sync = mem(() => {

    /*process.platform 判断操作系统，若是 OS X（即 darwin）或是 Linux，则执行 id -un 获取用户名；若是 Windows（即 win32），则执行 whoami 获取平台 & 用户名，再通过 cleanWinCmd 函数利用正则提取用户名。*/

	const envVar = getEnvVar();

	if (envVar) {
		return envVar;
	}

	if (os.userInfo) {
		return os.userInfo().username;
	}

	try {
		if (process.platform === 'win32') {
			return cleanWinCmd(execa.sync('whoami').stdout);
		}

		return execa.sync('id', ['-un']).stdout;
	} catch (_) {}
});

```

# 最后 #

1. SUDO_USER 与 USER 变量的区别
	1. 当用户身份是 root 时，此时的 USER 变量会返回 root，而 SUDO_USER 变量返回的是登陆为 root 的账户名，例如：当我以 elvin 账户通过 sudo su 变为 root 用户后，USER 会返回 root，SUDO_USER 会返回 elvin。
2. Node.js 中 process.env 增删查改
	1. process.env.foo = {};
	2. delete process.env.foo
3. os.userInfo() 返回的信息；
	```
	const os = require('os');

	console.log(os.userInfo());
	
	// => {
	// => 	uid: 501,
	// => 	gid: 20,
	// => 	username: 'elvin',
	// => 	homedir: '/Users/elvin',
	// => 	shell: '/bin/zsh'
	// => }
	```
4. process.platform 返回的值不止 darwin | win32 | Linux，也许 username 这里能有更好的处理
5. noop 空函数在 Promise 出错时吞掉异常的优点。