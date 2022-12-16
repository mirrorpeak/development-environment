ARG REPO=mcr.microsoft.com/dotnet/sdk
FROM $REPO:7.0-jammy

RUN yes | unminimize \
    && apt-get update && apt-get upgrade \
    && apt-get install -y \
    bat \
    exa \
    man-db \
    nano \
    openssh-server \
    sudo \
    unzip \
    zsh \
    && ln -s /usr/bin/batcat /usr/bin/bat

RUN DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install -y tzdata

#RUN service ssh start
#RUN /usr/sbin/sshd

RUN adduser --home /home/developer --shell /usr/bin/zsh --ingroup root developer \
    && usermod -a -G sudo developer \
    && passwd -d developer

USER developer
WORKDIR /home/developer

RUN yes | sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" \ 
    && git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions \
    && git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting \
    && sed -i '/^ZSH_THEME="robbyrussell"/c\ZSH_THEME="gnzh"' .zshrc \
    && sed -i '/^plugins=/c\plugins=(git zsh-autosuggestions zsh-syntax-highlighting)' .zshrc \
    && echo 'alias ll="exa -l -g --icons"' >> .zshrc \
    && echo 'alias ls="exa --icons"' >> .zshrc \
    && echo 'alias lt="exa --tree --icons -a"'  >> .zshrc

CMD ["zsh"]
