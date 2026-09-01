# Dotfiles

Collection of configuration files I use in my WSL installation. Storing these files together makes them easy to version control. However, dotfiles like .gitconfig and .zshrc are assumed to be in the home directory, /home/<username>. I therefore use [stow](https://www.gnu.org/software/stow/) to create symlinks in the home directory which links back to the files stored in this directory, i.e. `/home/<username>/.gitconfig -> dotfiles/git/.gitconfig`.

The organisation of the files in this directory is important. Each dotfile or collection of dotfiles is placed in a folder - .gitconfig is for example placed in git/. Then the symlinks are established through

```bash
stow <folder-name>
```

So for example, `stow git` to establish the symlink between `~/.gitconfig` and `dotfiles/git/.gitconfig`. When doing `stow <folder-name>`, stow adopts the same hierarchy as in the given folder when it establishes symlinks. So for dotfiles that are expected to exist in a subfolder in the home directory, the expected folder structure needs to be mirrored in the dotfiles directory. For example, a dotfile expected to reside in `~/.config/.exampledotfile`, will need to be symlinked to the following file in dotfiles `dotfiles/config/.config/.exampledotfile`. When executing `stow config`, stow copies the hierarchy existing in the config folder into the home directory.
