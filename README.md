# NEST Desktop Apptainer

It contains Apptainer recipes for NEST Desktop and NEST Simulator containers. Note that Apptainer runs only on Linux systems.

For more information, please see the
[User Documentation Page of NEST Desktop](https://nest-desktop.readthedocs.io)
as well as the
[User Documentation Page of NEST Simulator](https://nest-simulator.readthedocs.io).

## Security considerations

The `/exec` route of the NEST Server API allows you to run custom Python scripts within the NEST Server context. This can greatly simplify your workflow in situations where you already have the simulation description in the form of a Python script. On the technical side, however, this route exposes a potential risk for the remote execution of malicious code.

## Preparation

#### Requirements

- Apptainer 1.0 or higher

To install Apptainer, please follow [the official installation guide of Apptainer page](https://github.com/apptainer/apptainer/blob/main/INSTALL.md).

#### Installation

##### 1. Clone a working copy from the repository:

```
git clone https://github.com/nest-desktop/nest-desktop-apptainer
cd nest-desktop-apptainer
```

##### 2. Register the command `nest-desktop-apptainer`:

```
export PATH=$PATH:$PWD/bin
```

> | :information_source: **Info** |
> | ----------------------------- |
>
>
> Please keep in mind, that these changes are only temporary. If you would like to keep these permanently, you need to add the command to your `.profile` configuration file.
> `echo "export PATH=$PATH:$PWD/bin" >> ~/.profile`
> After that, you need to relogin (or restart), so that the changes are adopted.

##### 3a. Build the Apptainer containers for NEST Desktop and NEST Simulator (with `sudo`):

```
nest-desktop-apptainer build
```

Then, it creates two image files (`nest-desktop.sif` and `nest-simulator.sif`) in the `images` subfolder.

#### 3b. Alternative: you can use fakeroot to build containers.

Add your username to the Apptainer fakeroot config.

```
sudo apptainer config fakeroot --add $USER
```

Then you can build containers with fakeroot (without `sudo`) in the future (e.g. when a container received updates). If you have not removed the containers before, you will be asked for confirmation before these are overwritten (`y` to confirm, `N` to abort). This is not necessary directly after the installation! If you copied this command and executed it thoughtlessly, no worries: This is not harmful, it is only inefficient to rebuild the freshly built containers.

```
nest-desktop-apptainer build -f
```

## Usage

Start the instances of NEST Desktop and NEST Simulator:

```
nest-desktop-apptainer start
```

Now, **NEST Desktop** is serving at [`localhost:54286`](localhost:54286)
<br/>
and **NEST Simulator** at [`localhost:52425`](localhost:52425).

#### Further methods

Get the status of both instances.

```
nest-desktop-apptainer status
```

Stop both instances.

```
nest-desktop-apptainer stop
```

Restart both instances.

```
nest-desktop-apptainer restart
```

For more commands of Apptainer, please consult the [official documentation](https://apptainer.org/docs/user/main/cli.html).

#### Execute a command for a single instance

Start a single container, e.g. NEST Desktop.

```
nest-desktop-apptainer start nest-desktop
```

Restart a single container, e.g. NEST Simulator.

```
nest-desktop-apptainer restart nest-simulator
```

### License

Licensed under the [MIT](LICENSE) license.
