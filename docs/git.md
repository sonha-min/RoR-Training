## What is Git?

- Git is a **distributed version control system** — each person has a full copy of the repository on their own computer.
- Git allows multiple people to work on the same project **without needing to be constantly connected to each other or to a central server.**
- Git keeps **track of the entire history of changes**, making it easy to **go back to previous versions** if needed.
- **Repository**: Stores the full history of commits and tracks all changes made to the codebase.

## Git Workflow

- **Working directory**: It’s your local workspace, where you make changes directly to files.
- **Staging area**: A middle layer that holds changes you’ve prepared to commit. You can selectively add or remove changes in the staging area before committing —> giving you precise control over what gets saved to version history.
- **Local repository**: A version of the repository stored on your local machine. It contains the full history of commits and allows you to work offline.
- **Remote repository**: A version of the repository hosted on a server (e.g., GitHub, GitLab, Bitbucket). It enables collaboration by letting multiple people clone the code, push their changes, and pull updates from others.

![Git Space](https://github.com/vosonha/RoR-Training/blob/main/lib/images/gitWorkflow.png)

## Git branch

Trong Git có 3 lớp chính:
| Mức | Mô tả |
| ---------------------------- | -------------------------------------------------------------- |
| ✅ **Remote branch** | Branch trên server thực sự chứa dữ liệu (`github.com`, `gitlab.com`, `bitbucket` v.v.) |
| ✅ **Remote-tracking branch** | Như `origin/main`, `origin/feature1` trên máy (cache) |
| ✅ **Local branch** | Như `main`, `feature1` — nơi làm việc thực tế |

## Steps for working on a project

### Create SSH key

- Generate ssh key: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

  ```bash
  ssh-keygen -t ed25519 -C "your_email@example.com"
  ```

- Add public key to github: https://github.com/settings/keys

- Config file `~/.ssh/config`:

  ```
  Host github_havs => alias, đặt tùy thích, đặt gì thì khi clone code phải sử dụng như vậy
    HostName github.com => domain thật sự của git server sử dụng
    User git => mặc định, ko chỉnh sửa
    IdentityFile ~/.ssh/havs/id_rsa_havs => file private key pair với public key đã đăng ký
  ```

**Note:** Configure multiple ssh keys

- Generate keys => should create sub folder for each key

- Add public keys to github accounts

- Config file `~/.ssh/config`

### Clone repo and configure git

- Clone repo: `git clone <git-url>`

  ```bash
  git clone git@github_havs:vosonha/RoR-Training.git
  ```

- Git config user name and email:

  - Global config -> applies to all repositories on your machine.

    ```bash
    git config --global user.name <name>
    git config --global user.email <email>
    ```

  - Remove global config:

    ```bash
      git config --global --unset <key>
    ```

  - Local config -> applies only to the current repository.
    ```bash
    git config --local user.name <name>
    git config --local user.email <email>
    ```

- View config: `git config --list`
- Git settings folder: `.git/`

### Working on branch

- View local branches and current branch: `git branch`

- Create new branch: `git checkout -b <branch name>` (`-B` create new branch or reset existing branch)

- Make changes -> add + commit -> push:

  - `git add <files>` or `git add .`

  - `git commit -m '<your message>'`

  - `git push [-u] <remote name> <local branch>:<remote branch>`

    - `git push` -> push to upstream (it will raise error if upstream is not set)

      - Set upstream branch for current branch:

        ```bash
          git branch --set-upstream-to=<remote>/<branch>
        ```

      - Unset upstream branch for current branch:

        ```bash
          git branch --unset-upstream
        ```

    - `git push origin` -> push to remote branch on remote origin

    - `git push origin feature2` -> push local branch feature2 to remote branch feature2 on remote origin

    - `git push origin feature1:feature2` -> push local branch feature1 to remote branch feature2 on remote origin => ko khuyến khích

    - `git push origin :feature1` -> delete remote branch feature1 on remote origin

- Pull code:

  - `git pull` = `git fetch` + `git merge/rebase`

    **Note:**

    ```bash
      - raise error if local branch is not set upstream branch.
      - if local branch is set upstream branch, it will pull code from remote branch to local branch.
    ```

  - `git pull origin <branch name>` -> pull code from remote branch to local branch

  - `git fetch` -> `git merge <branch name>` or `git rebase <branch name>`

    - **Note:** git rebase: sử dụng trên nhánh private (làm 1 mình). Không sử dụng trên nhánh làm chung or nhánh làm một mình bà rebase báo conflict 2 lần.

## Notes

- Luôn kiểm tra trạng thái của repository bằng `git status` trước khi thực hiện commit hoặc push.
- Sử dụng `git log` để xem lịch sử commit và kiểm tra các thay đổi đã được lưu.
- Khi làm việc với nhiều người, hãy thường xuyên pull code để tránh conflict.
- Nếu xảy ra conflict, hãy giải quyết trước khi tiếp tục làm việc.

### Resolve conflict (conflict xảy ra khi merge/rebase mà có code trong 1 file khác version):

- Lựa chọn:

  ```bash
    - Bỏ code mình (1)
    - Bỏ code người ta (2)
    - Giữ cả 2 (có thể modify) (3)
  ```

=> Đọc code tự tin thì chọn (1) or (2) or (3). Ko tự tin thì kiếm người tạo ra commit conflict với mình để discuss và giải quyết.

- Giải quyết:

  ```bash
    - Sửa file(s) bị conflict
    - git add <file(s)>
    - git commit -m <message>
    - git push
  ```

### git merge vs git rebase

https://blog.git-init.com/differences-between-git-merge-and-rebase-and-why-you-should-care/

Example:

- History commit:

  ```bash
    A---B---C  (main)
        \
          D---E---F  (feature)
  ```

- `git merge feature` (từ `main`)

  ```bash
    A---B---C-------G   (main)
        \          /
          D---E---F     (feature)
  ```

  `-> G là merge commit`

- `git rebase main` (từ `feature`)

  ```bash
    A---B---C---D'---E'---F'  (feature)
  ```

  `-> D', E', F' là các commit mới, không có merge commit`

## Common commands

- `git stash`: tạm thời bỏ những thay đổi lên stash để chuyển nhánh.

  - `git stash list`: view stashed list
  - `git stash apply`: apply thay đổi, vẫn giữ lại code changes trên stash
  - `git stash pop`: apply and pop code change trên stash
    https://git-scm.com/docs/git-stash#_description

- `git checkout`:

  - Chuyển nhánh: `git checkout <branch_name>`
  - Chuyển version file: `git checkout <commit_id>|<branch_name> <file_name>`
  - Tạo nhánh mới: `git checkout -b <new_branch_name>`

- `git status` -> provide info: current branch, file untracked, file modified, file ready to commit, conflict.

- `git reset`:

  - `--mix` (default): bỏ lịch sử, giữ code, ko add changes vào index

  - `--soft`: bỏ lịch sử, giữ code

  - `--hard`: bỏ code, bỏ lịch sử

- `git config`:

  - `git config [scope] <key> <value>`: set config
  - `git config --unset <key>`: remove config
  - `git config --list`: view all config

- `git remote`:

  - `git remote -v`: view remote list
  - `git remote remove <remote name>`: remove remote
  - `git remote add <remote name> git@alias_name:git_repo_path`: add remote

## GUI tool

- Git cola:

  - view status of branch + support full commands (commit, push, pull...)

  - review change trước khi commit

  - commit 1 phần file hay revert change dễ dàng

- gitk: view history

- Git cheat sheet: https://education.github.com/git-cheat-sheet-education.pdf
