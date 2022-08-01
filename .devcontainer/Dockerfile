FROM frankfang128/oh-my-docker:mangosteen

RUN yes | pacman -S unzip && curl https://bun.sh/install | bash

# Rust
WORKDIR /tmp
RUN mkdir -p /root/.cargo ; echo -e $"\
[source.crates-io]\n\
replace-with = 'ustc'\n\
[source.ustc]\n\
registry = 'git://mirrors.ustc.edu.cn/crates.io-index'\n\
" > /root/.cargo/config
ENV RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static
ENV RUSTUP_UPDATE_ROOT=https://mirrors.ustc.edu.cn/rust-static/rustup
ENV CARGO_HTTP_MULTIPLEXING=false
ENV PATH="/root/.cargo/bin:${PATH}"
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y
# end

