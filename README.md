# piping.sh

Allows you to use an SSH server as a piping-server.
This is inspired from:

 * https://github.com/nwtgck/piping-server
 * https://gist.github.com/nakamuray/f70221e02862f6ed526873d3996a1644

## Usage

### Preparation

1. Setup an SSH server.
2. Put the `piping` at `/usr/local/bin/piping` or somewhere.


### Basic usage

Assume that you already setup a relay server as `my-ssh-server`.

On a sender host, you may give any data to your relay server via a pipeline, as:

```console
user@sender-host:~$ seq 1 3 | ssh user@my-ssh-server piping seq
```

On this case, `piping` is the command name and the argument `seq` is the name of the pipeline. If there is no existing pipeline with the name, `piping` starts in the writing mode. Othwrwise the command starts in the reading mode for a receiver. Ths, on a receiver host, you may receive any data from your relay server via a pipeline, as:

```console
user@receiver-host:~$ ssh user@my-ssh-server piping seq
1
2
3
```

### Additional usage

If you give no pipeline name, `piping` generates random name for a new pipeline and starts in the writing mode:

```console
user@sender-host:~$ seq 1 3 | ssh user@my-ssh-server piping
A pipeline is prepared as "K6JK2"
```

On this case, `K6JK2` is the name of the pipeline. Then you will need to specify the generated name on the receiver, like:

```console
user@receiver-host:~$ ssh user@my-ssh-server piping K6JK2
1
2
3
```


