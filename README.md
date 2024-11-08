# svim
svim is a Bash script designed to help you manage multiple configurations for Neovim. It allows you to create, switch between, and manage different Neovim configurations conveniently.

## Usage guide
Copy script to `/usr/local/bin`, and set executive permission

### Options and Parameters
`-c`: (Optional) Indicates that you want to create a new configuration.

`-l`: (Optional) Lists all available configurations and displays the current configuration.

`-r <config>`: (Optional) Removes the specified configuration after confirmation.

`config`: (Required) The name of the configuration you want to create, switch to, or remove.

### Usage

#### Creating a New Configuration

To create a new Neovim configuration, use the `-c` option followed by the name of the configuration:

```bash
svim -c <config_name>
```
Example:

```bash
svim -c myconfig
```

What It Does:
Creates the following directories:
```bash
~/.config/nvim_<config_name>
~/.local/share/nvim_<config_name>
~/.cache/nvim_<config_name>
```
Creates symbolic links from these directories to the standard Neovim configuration directories:
```
~/.config/nvim
~/.local/share/nvim
~/.cache/nvim
```
>[!NOTE]
>If any of the configuration directories already exist, the script will output an error message and exit without making changes.

#### Switching to an Existing Configuration

To switch to an existing configuration, omit the -c option and provide the configuration name:

```bash
svim <config_name>
```
Example:

```bash
svim myconfig
```
What It Does:

Checks if the configuration directories exist:
```bash
~/.config/nvim_<config_name>
~/.local/share/nvim_<config_name>
~/.cache/nvim_<config_name>
```
If they exist, updates the symbolic links to point to these directories.

If any of the directories do not exist, the script outputs an error message and exits.

#### Listing Configurations

To list all available configurations and display the current one, use the `-l` option:

```bash
svim -l
```

What It Does:
- Displays all configurations found in `~/.config/` with the prefix `nvim_`.
- Shows the currently active configuration if one is set.

#### Removing a Configuration

To remove a specific configuration, use the `-r` option followed by the configuration name:

```bash
svim -r <config_name>
```

What It Does:
- Prompts for confirmation by asking the user to enter the configuration name twice.
- Deletes the specified configuration directories if confirmed.

### Error Handling:

If the required config parameter is missing, the script will display usage information and exit.
When creating a new configuration with `-c`, if the target configuration directories already exist, the script will inform you and terminate to prevent overwriting existing configurations.
When switching configurations without `-c`, if the specified configuration directories do not exist, the script will notify you of the missing directories and exit.
When removing a configuration, if the specified configuration does not exist, the script will notify you and exit.

#### Symbolic Links:

The script manages symbolic links for Neovim's configuration directories. It removes existing links before creating new ones to ensure they point to the correct configuration.

### Examples

#### Create and Switch to a New Configuration Named dev:

```bash
svim -c dev
```
Creates:
```bash
~/.config/nvim_dev
~/.local/share/nvim_dev
~/.cache/nvim_dev
```
Updates symbolic links to point to these new directories.

#### Switch to an Existing Configuration Named work:

```bash
svim work
```
Updates symbolic links to point to:
```bash
~/.config/nvim_work
~/.local/share/nvim_work
~/.cache/nvim_work
```

#### List All Configurations and Current Configuration:

```bash
svim -l
```

Output Example:
```
Available configurations:
dev
work
Current configuration: dev
```

#### Remove a Configuration Named myconfig:

```bash
svim -r myconfig
```

Output Example:
```
Are you sure you want to remove the configuration 'myconfig'? (type it twice to confirm)
Enter configuration name: myconfig
Confirm configuration name: myconfig
Configuration 'myconfig' has been removed.
```

#### Error Scenario – Attempt to Create an Existing Configuration:

```bash
svim -c dev
```
Output:

```bash
Error: Configuration directories already exist.
```

## Summary
svim simplifies the process of managing multiple Neovim configurations by automating the creation and switching of configuration directories through symbolic links. This allows for a seamless experience when working with different setups, such as development, testing, or personal projects.
