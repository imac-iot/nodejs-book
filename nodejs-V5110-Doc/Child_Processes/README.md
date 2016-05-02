# Table of Contents

- [Child Process](#child-process)
  - [Asynchronous Process Creation](#asynchronous-process-creation)
    - [Spawning .bat and .cmd files on Windows](#spawning-bat-and-cmd-files-on-windows)
    - [child_process.exec(command[, options][, callback])](#child_processexeccommand-options-callback)
    - [child_process.execFile(file[, args][, options][, callback])](#child_processexecfilefile-args-options-callback)
    - [child_process.fork(modulePath[, args][, options])](#child_processforkmodulepath-args-options)
    - [child_process.spawn(command[, args][, options])](#child_processspawncommand-args-options)
      - [options.detached](#optionsdetached)
      - [options.stdio](#optionsstdio)
  - [Synchronous Process Creation](#synchronous-process-creation)
    - [child_process.execFileSync(file[, args][, options])](#child_processexecfilesyncfile-args-options)
    - [child_process.execSync(command[, options])](#child_processexecsynccommand-options)
    - [child_process.spawnSync(command[, args][, options])](#child_processspawnsynccommand-args-options)
  - [Class: ChildProcess](#class-childprocess)
    - [Event: 'close'](#event-close)
    - [Event: 'disconnect'](#event-disconnect)
    - [Event: 'error'](#event-error)
    - [Event: 'exit'](#event-exit)
    - [Event: 'message'](#event-message)
    - [child.connected](#childconnected)
    - [child.disconnect()](#childdisconnect)
    - [child.kill([signal])](#childkillsignal)
    - [child.pid](#childpid)
    - [child.send(message[, sendHandle[, options][, callback])](#childsendmessage-sendhandle-options-callback)
      - [Example: sending a server object](#example-sending-a-server-object)
      - [Example: sending a socket object](#example-sending-a-socket-object)
    - [child.stderr](#childstderr)
    - [child.stdin](#childstdin)
    - [child.stdio](#childstdio)
    - [child.stdout](#childstdout)
  - [maxBuffer and Unicode](#maxbuffer-and-unicode)


# Child Process
# Asynchronous Process Creation
### Spawning .bat and .cmd files on Windows
### child_process.exec(command[, options][, callback])
### child_process.execFile(file[, args][, options][, callback])
### child_process.fork(modulePath[, args][, options])
### child_process.spawn(command[, args][, options])
###### options.detached
###### options.stdio
# Synchronous Process Creation
### child_process.execFileSync(file[, args][, options])
### child_process.execSync(command[, options])
### child_process.spawnSync(command[, args][, options])
# Class: ChildProcess
### Event: 'close'
### Event: 'disconnect'
### Event: 'error'
### Event: 'exit'
### Event: 'message'
### child.connected
### child.disconnect()
### child.kill([signal])
### child.pid
### child.send(message[, sendHandle[, options]][, callback])
###### Example: sending a server object
###### Example: sending a socket object
### child.stderr
### child.stdin
### child.stdio
### child.stdout
# maxBuffer and Unicode