# Windows开发环境



> 基于 WSL2

---

1. 配置`WSL2`开发环境

   a. 管理员身份运行`powershell`

   b. 输入下面四条命令

   ```shell
   $ wsl --install
   $ dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   $ dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   $ wsl --set-default-version 2
   ```

   c. 重启电脑

   d. 安装`Ubuntu`指定发行版本，在`Microsoft Store`中直接搜索`ubuntu`，安装指定发行版本即可（安装wsl的时候会默认安装`不带任何发行版本的ubuntu`）

   e. 运行命令`wsl -d <Distro>`, 运行指定的分发版。如果上述步骤安装的是ubuntu-22.04，运行`wsl -d Ubuntu-22.04`。可以运行`wsl -l`查看已经安装了那些分发版本，然后选择运行指定分发版。

   

   错误处理：

   当遇到错误提示`参考对象类型不支持尝试的操作`时，可以运行以下命令

   `````shell
   $ netsh winsock reset
   `````

   当上述命令解决不了问题的时候，可以参考以下步骤

    1. 下载 [`nolsp.exe`](https://github.com/dyingsu/nolsp)

    2. 找到对应的下载目录，以管理员身份运行`powershell`

    3. 找到wsl的文件目录`搜索->wsl->打开文件所在位置`，复制文件目录

    4. 在`powershell`中执行命令

       ```shell
       $ .\NoLsp_fix_WSL2_参考的对象类型不支持尝试的操作.exe C:\windows\system32\wsl.exe
       ```

       其中`wsl.exe`的文件路径要换成真实的文件路径。

       执行完毕看到`Success!`即为成功。

   `Tips:`

   ​		当配置了代理后，可能还会遇到这样的情况，建议先装好代理环境，然后再执行上述操作，否则会容易导致代理失效。

   
---
   

2. 配置`VSCode`开发环境

   a. 下载安装 [`VSCode`](https://code.visualstudio.com/download)

   b. 安装插件

   ```
   - WSL（可以直接连接到WSL的ubuntu环境中）
   - Go
   ```

---  

3. 配置`Docker`

   a. 下载[`Docker`](https://docs.docker.com/desktop/install/windows-install/)

   b. 设置支持在`wsl`环境编译[参考文档](https://docs.docker.com/desktop/wsl/)

---

4. 配置`终端`

   a. 在`Microsoft Store`中直接搜索`Windows Terminal`安装

   b. 安装字体[字体下载](https://github.com/romkatv/powerlevel10k#fonts)，下载后双击安装

   c. 打开`Windows Terminal`设置，打开`JSON配置文件`，将`windows/configs/windows_terminal_settings.json`文件内容复制粘贴

   d. 打开`Windows Terminal`, 连接到运行的分发版终端，执行下面命令

   ```shell
   # 更换清华镜像源
   $ wget https://gitee.com/lin-xi-269/tools/raw/master/os/QHubuntu20.04 && bash QHubuntu20.04
   $ apt update
   $ apt upgrade	
   
   # 安装zsh
   $ apt install zsh
   
   # 设置默认shell为zsh
   $ chsh -s /bin/zsh
   
   # 安装ohmyzsh, 安装成功后，将 `windows/configs/zshrc.config` 文件内容复制粘贴到 `~/.zshrc`
   $ wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh
   $ sh install.sh
   
   # 安装p10k, 安装成功后，将 `windows/configs/p10k.config` 文件内容复制粘贴到 `~/.p10k.zsh`
   $ git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
   
   # 安装zsh插件
   [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)
   [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md#oh-my-zsh)
   
   # 安装kubectl [参考文档](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
   # 版本号与集群保持一致
   $ curl -LO https://dl.k8s.io/release/${版本号}/bin/linux/amd64/kubectl
   $ sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
   # 安装kubectl自动补全工具
   $ mkdir -p ~/.oh-my-zsh/custom/plugins/kubectl-autocomplete/
   $ kubectl completion zsh > ~/.oh-my-zsh/custom/plugins/kubectl-autocomplete/kubectl-autocomplete.plugin.zsh
   
   $ source ~/.zshrc
   
   # 配置Vim，将 `windows/configs/vimrc.config` 文件内容复制粘贴到 `~/.vimrc`
   # 安装插件
   # pathogen-vim
   $ mkdir -p ~/.vim/autoload ~/.vim/bundle && \
   curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
   # nerdtree-vim
   $ git clone https://github.com/preservim/nerdtree.git ~/.vim/bundle/nerdtree
   
   # 安装vscode命令行工具
   $ code .
   ```
   

   


