
## oxlint

代码质量检查。
- 支持：Javascript、Typescript、JSX、TSX、框架文件的`<script>`块。
- 编辑器插件：`Oxc VS Code`

```Shell
pnpm add -D oxlint
```

###### 常用命令

```Shell
# oxlint [OPTIONS] [PATH]...

oxlint --init # 初始化 `.oxlintrc.json` 配置
# 安全修复，其他参数：
# --fix-suggestions  应用建议修复（可能会改变程序行为）
# --fix-dangerously  应用危险修复和建议
oxlint --fix
oxlint --rules # 列出已注册的规则，包括当前 oxlint 配置启用的规则

oxlint --print-config path/to/file.ts # 打印文件进行lint时会使用到的配置
oxlint --ignore-pattern "dist/**" --ignore-pattern "*.min.js" # 从命令行添加忽略模式
```

###### .oxlintrc.json

- 嵌套配置文件：Oxlint 会使用与lint文件最近的配置；配置文件不会合并；子目录不影响父目录；命令行选项会覆盖所有配置；
- 扩展配置文件：文件可任意命名；只支持部分属性扩展：`rules`、`plugins`、`overrides`
- 插件：一组有名称的规则 [支持的插件](https://oxc.nodejs.cn/docs/guide/usage/linter/plugins.html#supported-plugins)
- 多文件分析：启用 [`import/no-cycle`](https://oxc.nodejs.cn/docs/guide/usage/linter/rules/import/no-cycle.html) 以检测循环依赖

```json
{
	// 编辑器工具的模式 URI
	"$schema": "./node_modules/oxlint/configuration_schema.json",
	// 扩展共享配置
	"extends": ["./configs/base.json", "./configs/frontend.json"],
	// 为常见环境（如浏览器或 Node）启用预定义的全局变量。接受：false、true、off
	"env": {
		"browser": true,
	    "node": true,
	    "es2024": true
	},
	// 启用或禁用规则：严重程度（"off|0|allow"、"warn|1"、"error|2|deny"）
	"rules": {
		"eslint/no-unused-vars": "error"
	},
	// 启用或禁用具有相似意图的一组规则
	"categories": {
		"correctness": "error", // 绝对错误或无用的代码
	    "suspicious": "warn" // 可能是错误或无用的代码
	},
	// 忽略文件：可使用!取消忽略指定文件
	"ignorePatterns": ["build/**/*", "!build/keep.js"],
	// 全局变量
	"globals": {
		"defineOptions": "readonly",
	    "defineProps": "readonly",
	    "defineEmits": "readonly",
	    "defineExpose": "readonly",
	    "withDefaults": "readonly"
	},
	// 按文件模式应用配置：将不同的配置应用到不同的文件，例如测试文件、脚本或仅限 TypeScript 的路径
	"overrides": [
		{
			"files": ["scripts/*.js"],
			"rules": { "no-console": "off" },
			"env": {},
			"globals": {},
			plugins: []
		},
		{
			"files": ["**/test/**"],
			"rules": {
				"jest/no-disabled-tests": "off"
			},
			"env": {
				"jest": true
			},
			plugins: ["jest"]
		}
	],
	// 使用插件扩展可用规则
	"plugins": ["eslint", "typescript", "unicorn", "oxc", "vue", "import"],
	// 插件设置
	"settings": {}
}
```

###### 行内注释

```js
// file
/* oxlint-disable */
/* oxlint-disable no-console */
/* oxlint-disable no-console, typescript/no-floating-promises */

// line
// oxlint-disable-line no-console
// oxlint-disable-next-line no-console
```

###### 输出格式

```Shell
oxlint --format|-f json # 选择输出格式，方便与CI/CD工具、第三方分析工具搭配使用。包括：`default`、`json`、`unix`、`checkstyle`、`github`、`gitlab`、`junit`、`stylish`
```

###### 从Eslint迁移

[参考文档](https://oxc.nodejs.cn/docs/guide/usage/linter/migrate-from-eslint.html)

## oxfmt

代码风格检查。

###### .oxfmtrc.json

[配置参考](https://oxc.nodejs.cn/docs/guide/usage/formatter/config-file-reference.html)

```json
{
	"$schema": "./node_modules/oxfmt/configuration_schema.json",
	"printWidth": 100, // 行宽限制
	"tabWidth": 2, // 缩进
	"useTabs": false, // 使用tabs代替space
	"semi": true, // 添加分号
	"singleQuote": true, // 使用单引号
	"trailingComma": "es5", // 多行结构中的尾随逗号
	"bracketSpacing": true,
	"arrowParens": "always",
	"proseWrap": "preserve",
	"htmlWhitespaceSensitivity": "css",
	"vueIndentScriptAndStyle": true,
	"endOfLine": "lf",
	"embeddedLanguageFormatting": "auto",
	"experimentalSortPackageJson": true, // package.json 排序（默认启用）
	"experimentalTailwindcss": true, // Tailwind 类排序
	"ignorePath": ".gitignore" // 排除格式化
}
```