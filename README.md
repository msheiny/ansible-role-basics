# ansible-role-sysbasics

A role to do basic system bootstrap:
    * installng pkgs,
    * configuring vim,
    * setting up zsh
    * gnome settings

Each tasks is pretty specific. I'm usually not a fan of all encompassing roles
but I don't think there is enough here to warrant a role per task.

## Default Vars

```
---

##### PACKAGING ###############################################
###############################################################
sysbasics_pkgs:
  - git
  - tmux
  - tree
  - htop

sysbasics_desktop_pkgs: []

##### SHELL ###################################################
###############################################################

sysbasics_zsh_pkgs:
  - zsh
sysbasics_ohmyzsh_repo: https://github.com/robbyrussell/oh-my-zsh
sysbasics_ohmyzsh_enable: true
sysbasics_ohmyzsh_plugins:
  - git
  - gem
  - last-working-directory
  - pip

##### DOTFILES ################################################
###############################################################

basic_dotfiles_homeshick_repo: https://github.com/andsens/homeshick
sysbasics_dotfiles_username: "{{ ansible_user_id }}"

sysbasics_dotfiles_repo_name: dotsheiny
sysbasics_dotfiles_repo_version: master
sysbasics_dotfiles_github_username: msheiny
sysbasics_dotfiles_repo_url: https://github.com/{{ sysbasics_dotfiles_github_username }}/{{ sysbasics_dotfiles_repo_name }}.git

sysbasics_dotfiles_force_clone: "{{ false if ansible_connection == 'local' else true }}"

# Shell config file to make edits to
sysbasics_dotfiles_shell_conf: .bashrc


##### VIM #####################################################
###############################################################
sysbasics_vim_vundle_repo: https://github.com/VundleVim/Vundle.vim

##### GNOME CONFIG ############################################
###############################################################
dconf_settings: {}

# Here is an example of feeding in gnome settings. The underlying
# module is a little weird and below is an example of quoting formats.
# Notice for strings are quoted double - "'string'" but booleans and other
# types only need a single quote
#dconf_settings:
#  /org/gnome/terminal/legacy:
#    mnemonics-enabled: "true"
#    menu-accelerator-enabled: "true"
#    schema-version: "uint32 3"
#    default-show-menubar: "false"
#    theme-variant: "'dark'"
```
