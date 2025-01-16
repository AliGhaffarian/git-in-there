# what the heck is this?
an script to automate backing up files with git
# how to use
- get the git-in-there
	```
	git clone https://github.com/AliGhaffarian/get-in-there
	```

- create a github repository for the backups
- do at least one push to the repository (otherwise the script may not perform as intended)
- add a [configuration](https://github.com/AliGhaffarian/git-in-there?tab=readme-ov-file#configuration) file
- run the script
  ```
  python3 git-in-there.py
  pip install -r requirements.txt
  ```

# configuration
git-in-there reads the TARGETS_FILE file to see what files are tracked and to which repository it needs to push them  
the configurations must be provided in [yaml](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html)  
the default name is targets.yaml 

## limitations
currently special path symbols like ~ are not supported  

## config fields


### targets(optional)
a list of relative paths for directory or file which is inside of the corresponding root
### no_target(optional) 
if is present the targets will be ignored and entire root directory will be backed up without prompting the user

either targets or no_target field must be provided

todo:check for the target being inside root by checking if it's path starts with root
if is not provided the user will be warned and prompted to back up the entire root directory, the prompt can be suppresed with no_target
### root
an absolute path in which targets reside  
**must be absolute path**
### repo
the repo to which the files will be pushed
### name(optional)
used to identify the individual backup configurations when telling the script the certain ones to use by using `--repos_to_backup` argument  

### config example:
```yaml
-
    name: "vim_conf"
    repo: "https://github.com/AliGhaffarian/vim_conf"
    targets:
      - ".vim"
      - ".vimrc"
      - ".viminfo"
      - ".config/coc"
    root: "/home/user"
- 
    repo: "https://github.com/AliGhaffarian/mylinux"
    targets:
      - "Documents/people"
      - "Documents/archive"
      - "Documents/vim_cheat_sheet.png"
      - "Documents/startup"
    root: "/home/user"
-
    repo: "https://github.com/AliGhaffarian/books"
    root: "/home/user/Documents/books"
    no-target: true
```
# TODO
- A `.ignore` file that tells the script to ignore the directory
- Optimize grouping files for upload

