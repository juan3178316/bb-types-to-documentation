---
title: "bb types to documentation - index"
description: "Get samples about how works the blockbench types plugin"
author: juan3178316
date: 2025-10-28
---

# Index.d.ts

### Content
+ [`Class Deletable`](#class-deletable)
+ [`Const isApp`](#const-isapp)
+ [`Type EventName`](#type-eventname)
+ [`Type IconString`](#type-iconstring)
+ [`Interface MessageBoxOptions`](#interface-messageboxoptions)
+ [`namespace Blockbench`](#namespace-blockbench)

---

# methods


## Class Deletable

`delete: () => void`

| deletable_sample.ts |
| --- |
```typescript
var new_content;
Plugin.register('pluginID', {
	title: 'Your plugin Name',
	author: 'Your name',
	description: 'Plugin description',
	icon: 'description',
	min_version: '5.0.0',
	max_version: Blockbench.version,
	version: '0.0.1',
	variant: 'both',
	onload() {
		new_content = new Action({
			id: "new_action",
			name: "Your custom Action name",
			icon: 'description',
			category: "file",
			click: function(event) {}
		});
		MenuBar.addAction(new_content,'file');
	},
	onunload() {
		MenuBar.removeAction('file');
		new_content.delete();
	}
});
```


## Const isApp

True if Blockbench runs as a native app

`const isApp: boolean`


## Type EventName

`type EventName = 'remove_animation' | 'display_animation_fram' | 'before_closing' | 'create_session' | 'join_session' | 'quit_session' | 'send_session_data' | 'receive_session_data' | 'user_joins_session' | 'user_leaves_session' | 'process_chat_message' | 'update_settings' | 'update_project_settings' | 'save_project' | 'load_project' | 'new_project' | 'reset_project' | 'close_project' | 'add_cube' | 'add_group' | 'update_selection' | 'update_keyframe_selection' | 'select_all' | 'added_to_selection' | 'invert_selection' | 'canvas_select' | 'canvas_click' | 'change_texture_path' | 'add_texture' | 'finish_edit' | 'finished_edit' | 'undo' | 'redo' | 'select_mode' | 'unselect_mode'`


## Type IconString

`type IconString = string;`


## Interface MessageBoxOptions

```typescript
interface MessageBoxOptions {
	/**
	 * Index of the confirm button within the buttons array
	 */
	confirm: number
	/**
	 * Index of the cancel button within the buttons array
	 */
	cancel: number
	buttons: string[]
	translateKey?: string
	title?: string
	message?: string
	icon?: string
	width: number
}
```

## Namespace Blockbench

```typescript
declare namespace Blockbench {
	const platform: 'web' | 'win32' | 'darwin' | 'linux'
	const version: string
	/**
	 * Time when Blockbench was opened
	 */
	const openTime: Date
	function reload(): void
	/**
	 * checks if Blockbench is newer than the specified version
	 * 
	 * @param version
	 * semver string
	 */
	function isNewerThan(version: string): boolean
	/**
	 * checks if Blockbench is older than the specified version
	 * 
	 * @param version
	 * semver string
	 */
	function isOlderThan(version: string): boolean
	/**
	 * Resolves an icon string as a HTML element
	 * @param icon 
	 * Material Icons, Fontawesome or custom icon string
	 * @param color 
	 * CSS color
	 */
	function getIconNode(icon: IconString, color?: string): HTMLElement
	/**
	 * Shows a passing message in the middle of the screen
	 * 
	 * @param message 
	 * Message
	 * @param time 
	 * Time in miliseconds that the message stays up
	 */
	function showQuickMessage(message: string, time?: number): void

	function showStatusMessage(message: string, time?: number): void

	function setStatusBarText(text?: string): void
	/**
	 * Set the value of a progress bar
	 * 
	 * @param progress 
	 * Progress of the bar between 0 and 1
	 * @param time 
	 * Time over which the bar is animated, in miliseconds
	 * @param bar
	 * ID of the bar element. If omitted, the main status bar will be selected
	 */
	function setProgress(progress: number, time?: number, bar?: string): void

	/**
	 * Opens a message box
	 */
	function showMessageBox(options: MessageBoxOptions, callback: (buttonID: number) => void): void

	function textPrompt(title: string, value: string, callback: (value: string) => void): void
	/**
	 * Opens the specified link in the browser or in a new tab
	 */
	function openLink(link: URL): void

	/**
	 * Shows a system notification
	 * @param title Title
	 * @param text Text
	 * @param icon Url or data url pointing to an icon. Defaults to Blockbench icon
	 */
	function notification(title: string, text: string, icon?: string): void
	/**
	 * Adds custom CSS code to Blockbench, globally. Returns an object that is deletable
	 * @param css CSS string
	 */
	function addCSS(css: string): Deletable

	function addFlag(flag: string): void
	function removeFlag(flag: string): void
	function hasFlag(flag: string): boolean

	function dispatchEvent(event_name: EventName, data: object): void

	function addListener(event_names: EventName, callback: (data: object) => void): void
	function on(event_names: EventName, callback: (data: object) => void): void

	function removeEventListener(event_names: EventName): void
}
```

| blockbench_sample.ts |
| --- |
```typescript
console.info(Blockbench.version);
```