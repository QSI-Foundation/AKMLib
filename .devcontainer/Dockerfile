FROM    debian:12

ENV     DEBIAN_FRONTEND=noninteractive

RUN     apt -- update && apt -y -- upgrade && apt -y -- install \
          bash-completion tmux vim git-lfs wget build-essential cmake

RUN     wget -- https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb && \
        dpkg -i -- packages-microsoft-prod.deb && \
        rm -f -- packages-microsoft-prod.deb && \
        apt -- update && \
        apt -y -- install dotnet-sdk-8.0
