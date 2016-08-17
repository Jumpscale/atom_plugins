![screenshot from 2016-08-14 16-55-52](https://cloud.githubusercontent.com/assets/64129/17649980/b095dbe0-6249-11e6-95ff-d6a6d8eddb17.png)

1- Generate package `Packages -> Package generator` -> will set package name to execjs
2- Add to context menu by editing menus/execjs.cson
```coffeescript
# See https://atom.io/docs/latest/hacking-atom-package-word-count#menus for more details
'context-menu':

  'atom-text-editor': [
    {
      'label': 'Toggle execjs'
      'command': 'execjs:toggle'
    }
  ]
  '.tree-view.full-menu': [
      'label': 'JumpScale Commands'
      'submenu': [
        #   { 'label': 'run wc', 'command': 'execjs:runwc'}
          { 'label': 'Toggle execjs', 'command': 'execjs:toggle' }
          { 'label': 'runwc', 'command': 'execjs:runwc' }
          { 'label': 'mktidy', 'command': 'execjs:mktidy' }

      ]
  ]
```

3- In execjs.coffee
here are three commands
* toggle
* runwc -> to execute wc command
* mktidy -> to execute j.tools.markdown.tidy on selected path.
```coffeescript
ExecjsView = require './execjs-view'
subproc = require 'child_process'

{CompositeDisposable} = require 'atom'

module.exports = Execjs =
  execjsView: null
  modalPanel: null
  subscriptions: null

  activate: (state) ->
    @execjsView = new ExecjsView(state.execjsViewState)
    @modalPanel = atom.workspace.addModalPanel(item: @execjsView.getElement(), visible: false)

    # Events subscribed to in atom's system can be easily cleaned up with a CompositeDisposable
    @subscriptions = new CompositeDisposable

    # Register command that toggles this view
    @subscriptions.add atom.commands.add 'atom-workspace', 'execjs:toggle': => @toggle()
    # @subscriptions.add atom.commands.add 'atom-workspace', 'execjs:runwc' : => @runwc()

    @runwc = @runwc.bind(this)
    atom.commands.add '.tree-view .file .name', 'execjs:runwc', @runwc

    @mktidy = @mktidy.bind(this)
    atom.commands.add '.tree-view .entry', 'execjs:mktidy', @mktidy

  deactivate: ->
    @modalPanel.destroy()
    @subscriptions.dispose()
    @execjsView.destroy()

  serialize: ->
    execjsViewState: @execjsView.serialize()

  toggle: ->
      console.log "Hello"

  runwc: ({target}) ->
    filePath = target.dataset.path
    return unless filePath
    console.log filePath
    subproc.exec "wc #{filePath}", (err, stdout, sdterr) -> console.log stdout
    if @modalPanel.isVisible()
        @modalPanel.hide()
    else
        @modalPanel.show()
        setTimeout (@modalPanel.hide.bind(@modalPanel)), 2000
  mktidy: ({target}) ->
    filePath = target.dataset.path
    return unless filePath
    console.log filePath
    cmd = "jspython -c 'from JumpScale import j; j.tools.markdown.tidy(\"#{filePath}\")'"
    console.log "CMD #{cmd}"
    subproc.exec cmd, (err, stdout, sdterr) -> console.log stdout
    if @modalPanel.isVisible()
        @modalPanel.hide()
    else
        @modalPanel.show()
        setTimeout (@modalPanel.hide.bind(@modalPanel)), 2000

```
