FROM ubuntu:20.04
SHELL ["/bin/bash", "-c"]
RUN apt update
RUN apt list --upgradable
ENV LANG=C.UTF-8

RUN apt install -y curl git build-essential libssl-dev libreadline-dev zlib1g-dev libsqlite3-dev
RUN git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.8.1

RUN echo ". ~/.asdf/asdf.sh" >> ~/.bashrc
RUN echo ". ~/.asdf/completions/asdf.bash" >> ~/.bashrc
ENV PATH="/root/.asdf/bin:/root/.asdf/shims:${PATH}"

RUN asdf plugin add ruby https://github.com/asdf-vm/asdf-ruby.git
RUN asdf plugin add nodejs https://github.com/asdf-vm/asdf-nodejs.git

RUN asdf install nodejs 14.19.0
RUN asdf global nodejs 14.19.0

RUN asdf install ruby 2.6.9
RUN asdf global ruby 2.6.9

RUN gem install bundler -v 2.2.30
RUN gem install mailcatcher
RUN npm install -g yarn

EXPOSE 3000/tcp 1025/tcp 1080/tcp

CMD mkdir /app

WORKDIR /app

CMD tail -f
