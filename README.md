
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-5-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->

Godot Console
============

In-game console for Godot, easily extensible with new commands.

![Screenshot of in-game console for Godot](https://github.com/QuentinCaffeino/godot-console/blob/dev/screenshot.png)

## Features

- Writing to console using `write` and `writeLine` method. You can use [BB codes](https://godot.readthedocs.io/en/latest/learning/features/gui/bbcode_in_richtextlabel.html?highlight=richtextlabel#reference). (Also printed to engine output)

	`Console.writeLine('Hello world!')`

- <strike>Auto-completion on `TAB` (complete command)</strike> (broken right now), `Enter` (complete and execute).
- History (by default using with actions `ui_up` and `ui_down`)
- Custom types (`Filter`, `IntRange`, `FloatRange`, [and more...](https://github.com/QuentinCaffeino/godot-console/blob/dev/docs/Type/Type.md))
- [Logging](https://github.com/QuentinCaffeino/godot-console/tree/master/docs/Log.md)
- [FuncRef](https://docs.godotengine.org/en/3.2/classes/class_funcref.html) support with Godot >=3.2 (command target).

## Installation

1. Clone or download this repository to your project `res://addons/quentincaffeino-console` folder.
2. Enable console in Project/Addons
3. Add new actions to Input Map: `console_toggle`, `ui_up`, `ui_down`

## Example:

### Usage we will get:

```
$ sayHello "Adam Smith"
```

### Example function that will be called by our command:

```gdscript
func printHello(name = ''):
	Console.writeLine('Hello ' + name + '!')
```

### Registering command:

#### The new way (beta)

```gdscript
func _ready():
	# 1. argument is command name
	# 2. arg. is target (target could be a funcref)
	# 3. arg. is target name (name is not required if it is the same as first arg or target is a funcref)
	Console.addCommand('sayHello', self, 'printHello')\
		.setDescription('Prints "Hello %name%!"')\
		.addArgument('name', TYPE_STRING)\
		.register()
```

#### The old way (will be deprecated and later removed)

```gdscript
func _ready():
	Console.register('sayHello', { # Command name

		'description': 'Prints "Hello %name%!"',

		# This argument is obsolete if target function doesn't take any arguments.
		# If target is a variable then it takes one argument to set it, and zero to get its value.
		# You can fild more about how argument should look like below.
		# ARGUMENT[]
		'args': [[ 'name', TYPE_STRING ]],

		# Target to bind command to.
		# Providing name is obsolete if it is same as a command name.
			# [Object, variable/method name]
		'target': [ self, 'printHello' ]

	})
```

***ARGUMENT*** should look like this:
- [ 'arg_name', [**ARG_TYPE**](https://github.com/QuentinCaffeino/godot-console/blob/dev/docs/Type/Type.md) ]
- 'arg_name' — In this situation type will be set to Any
- [**ARG_TYPE**](https://github.com/QuentinCaffeino/godot-console/blob/dev/docs/Type/Type.md)

More information about [**ARG_TYPE**](https://github.com/QuentinCaffeino/godot-console/blob/dev/docs/Type/Type.md) you can find [here](https://github.com/QuentinCaffeino/godot-console/blob/dev/docs/Type/Type.md).

More examples in [`src/BaseCommands.gd`](https://github.com/QuentinCaffeino/godot-console/blob/dev/src/Misc/BaseCommands.gd)

----------

Great thanks to [@Krakean](https://github.com/Krakean) and [@DmitriySalnikov](https://github.com/DmitriySalnikov) for the motivation to keep improving the [original](https://github.com/Calinou/godot-console) console by [@Calinou](https://github.com/Calinou).

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="http://gitlab.com/QuentinCaffeino"><img src="https://avatars3.githubusercontent.com/u/2855777?v=4" width="100px;" alt=""/><br /><sub><b>Sergei ZH</b></sub></a><br /><a href="https://github.com/quentincaffeino/godot-console/commits?author=quentincaffeino" title="Code">💻</a> <a href="#question-quentincaffeino" title="Answering Questions">💬</a> <a href="https://github.com/quentincaffeino/godot-console/commits?author=quentincaffeino" title="Documentation">📖</a> <a href="#ideas-quentincaffeino" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/quentincaffeino/godot-console/pulls?q=is%3Apr+reviewed-by%3Aquentincaffeino" title="Reviewed Pull Requests">👀</a></td>
    <td align="center"><a href="http://www.underflowstudios.com"><img src="https://avatars3.githubusercontent.com/u/420072?v=4" width="100px;" alt=""/><br /><sub><b>Michael Brune</b></sub></a><br /><a href="#a11y-MJBrune" title="Accessibility">️️️️♿️</a> <a href="https://github.com/quentincaffeino/godot-console/issues?q=author%3AMJBrune" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/aganm"><img src="https://avatars0.githubusercontent.com/u/20380758?v=4" width="100px;" alt=""/><br /><sub><b>Michael Aganier</b></sub></a><br /><a href="https://github.com/quentincaffeino/godot-console/issues?q=author%3Aaganm" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/hpn33"><img src="https://avatars1.githubusercontent.com/u/16251202?v=4" width="100px;" alt=""/><br /><sub><b>hpn332</b></sub></a><br /><a href="https://github.com/quentincaffeino/godot-console/issues?q=author%3Ahpn33" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/danilw"><img src="https://avatars1.githubusercontent.com/u/24825887?v=4" width="100px;" alt=""/><br /><sub><b>Danil</b></sub></a><br /><a href="https://github.com/quentincaffeino/godot-console/issues?q=author%3Adanilw" title="Bug reports">🐛</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!

## License

Licensed under the MIT license, see `LICENSE.md` for more information.
