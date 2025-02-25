FROM fedora:latest
ARG GIT_REPO_URL="https://git.kernel.org/pub/scm/linux/kernel/git/axboe/blktrace.git"
ARG PROJECT="blktrace"
LABEL author="Hiroaki.Mihara"

RUN \
  dnf update -y && \
  dnf install -y \
    python3 \
    python3-pip \
    python3-jinja2 \
    python3-falcon \
    python3-bsddb3 \
    python3-pytest \
    perl \
    git \
    httpd \
    python3-mod_wsgi \
    jansson \
    libyaml \
    wget

# RUN \
#   pip3 install falcon

# RUN \
#   wget https://bootlin.com/pub/elixir/universal-ctags-0+git~20e934e3-1.6.x86_64.rpm --no-check-certificate

# RUN \
#   rpm -iv universal-ctags-0+git~20e934e3-1.6.x86_64.rpm

# RUN \
#   ln -s /var/lib/snapd/snap /snap

# RUN \
#   snap install universal-ctags

RUN \
  wget https://bootlin.com/pub/elixir/Pygments-2.6.1.elixir-py3-none-any.whl --no-check-certificate

RUN \
  pip3 install Pygments-2.6.1.elixir-py3-none-any.whl

RUN \
  git clone https://github.com/miharahiro/elixir.git /usr/local/elixir/

ENV LXR_REPO_DIR /srv/elixir-data/$PROJECT/repo
ENV LXR_DATA_DIR /srv/elixir-data/$PROJECT/data

# apache elixir config, see elixir README
# make apache less stricter about cgitb spam headers
RUN \
## Document Root = kernel
## Document Root = kernel
#  echo PERpcmVjdG9yeSAvdXNyL2xvY2FsL2VsaXhpci9odHRwLz4KICAgIE9wdGlvbnMgK0V4ZWNDR0kKICAgIEFsbG93T3ZlcnJpZGUgTm9uZQogICAgUmVxdWlyZSBhbGwgZ3JhbnRlZAogICAgU2V0RW52IFBZVEhPTklPRU5DT0RJTkcgdXRmLTgKICAgIFNldEVudiBMWFJfUFJPSl9ESVIgL3Nydi9lbGl4aXItZGF0YQo8L0RpcmVjdG9yeT4KPERpcmVjdG9yeSAvdXNyL2xvY2FsL2VsaXhpci9hcGkvPgogICAgU2V0SGFuZGxlciB3c2dpLXNjcmlwdAogICAgUmVxdWlyZSBhbGwgZ3JhbnRlZAogICAgU2V0RW52IFBZVEhPTklPRU5DT0RJTkcgdXRmLTgKICAgIFNldEVudiBMWFJfUFJPSl9ESVIgL3Nydi9lbGl4aXItZGF0YQo8L0RpcmVjdG9yeT4KQWRkSGFuZGxlciBjZ2ktc2NyaXB0IC5weQo8VmlydHVhbEhvc3QgKjo4MDgwPgogICAgU2VydmVyTmFtZSBNWV9MT0NBTF9JUAogICAgRG9jdW1lbnRSb290IC91c3IvbG9jYWwvZWxpeGlyL2h0dHAKICAgIFdTR0lTY3JpcHRBbGlhcyAvYXBpIC91c3IvbG9jYWwvZWxpeGlyL2FwaS9hcGkucHkKICAgIEFsbG93RW5jb2RlZFNsYXNoZXMgT24KICAgIFJld3JpdGVFbmdpbmUgb24KICAgIFJld3JpdGVSdWxlICJeLyQiICIva2VybmVsL2xhdGVzdC9zb3VyY2UiIFtSXQogICAgUmV3cml0ZVJ1bGUgIl4vKD8hYXBpfGFjcCkuKi8oc291cmNlfGlkZW50fHNlYXJjaCkiICIvd2ViLnB5IiBbUFRdCiAgICBSZXdyaXRlUnVsZSAiXi9hY3AiICIvYXV0b2NvbXBsZXRlLnB5IiBbUFRdCjwvVmlydHVhbEhvc3Q+ | base64 -d > /etc/httpd/conf.d/000-elixir.conf \

echo PERpcmVjdG9yeSAvdXNyL2xvY2FsL2VsaXhpci9odHRwLz4KICAgIE9wdGlvbnMgK0V4ZWNDR0kKICAgIEFsbG93T3ZlcnJpZGUgTm9uZQogICAgUmVxdWlyZSBhbGwgZ3JhbnRlZAogICAgU2V0RW52IFBZVEhPTklPRU5DT0RJTkcgdXRmLTgKICAgIFNldEVudiBMWFJfUFJPSl9ESVIgL3Nydi9lbGl4aXItZGF0YQo8L0RpcmVjdG9yeT4KPERpcmVjdG9yeSAvdXNyL2xvY2FsL2VsaXhpci9hcGkvPgogICAgU2V0SGFuZGxlciB3c2dpLXNjcmlwdAogICAgUmVxdWlyZSBhbGwgZ3JhbnRlZAogICAgU2V0RW52IFBZVEhPTklPRU5DT0RJTkcgdXRmLTgKICAgIFNldEVudiBMWFJfUFJPSl9ESVIgL3Nydi9lbGl4aXItZGF0YQo8L0RpcmVjdG9yeT4KQWRkSGFuZGxlciBjZ2ktc2NyaXB0IC5weQo8VmlydHVhbEhvc3QgKjo4MD4KICAgIFNlcnZlck5hbWUgTVlfTE9DQUxfSVAKICAgIERvY3VtZW50Um9vdCAvdXNyL2xvY2FsL2VsaXhpci9odHRwCiAgICBXU0dJU2NyaXB0QWxpYXMgL2FwaSAvdXNyL2xvY2FsL2VsaXhpci9hcGkvYXBpLnB5CiAgICBBbGxvd0VuY29kZWRTbGFzaGVzIE9uCiAgICBSZXdyaXRlRW5naW5lIG9uCiAgICBSZXdyaXRlUnVsZSAiXi8kIiAiL2tlcm5lbC9sYXRlc3Qvc291cmNlIiBbUl0KICAgIFJld3JpdGVSdWxlICJeLyg/IWFwaXxhY3ApLiovKHNvdXJjZXxpZGVudHxzZWFyY2gpIiAiL3dlYi5weSIgW1BUXQogICAgUmV3cml0ZVJ1bGUgIl4vYWNwIiAiL2F1dG9jb21wbGV0ZS5weSIgW1BUXQo8L1ZpcnR1YWxIb3N0Pgo= | base64 -d > /etc/httpd/conf.d/000-elixir.conf \
# Document Root = blktrace, port=80
#  echo PERpcmVjdG9yeSAvdXNyL2xvY2FsL2VsaXhpci9odHRwLz4KICAgIE9wdGlvbnMgK0V4ZWNDR0kKICAgIEFsbG93T3ZlcnJpZGUgTm9uZQogICAgUmVxdWlyZSBhbGwgZ3JhbnRlZAogICAgU2V0RW52IFBZVEhPTklPRU5DT0RJTkcgdXRmLTgKICAgIFNldEVudiBMWFJfUFJPSl9ESVIgL3Nydi9lbGl4aXItZGF0YQo8L0RpcmVjdG9yeT4KPERpcmVjdG9yeSAvdXNyL2xvY2FsL2VsaXhpci9hcGkvPgogICAgU2V0SGFuZGxlciB3c2dpLXNjcmlwdAogICAgUmVxdWlyZSBhbGwgZ3JhbnRlZAogICAgU2V0RW52IFBZVEhPTklPRU5DT0RJTkcgdXRmLTgKICAgIFNldEVudiBMWFJfUFJPSl9ESVIgL3Nydi9lbGl4aXItZGF0YQo8L0RpcmVjdG9yeT4KQWRkSGFuZGxlciBjZ2ktc2NyaXB0IC5weQo8VmlydHVhbEhvc3QgKjo4MD4KICAgIFNlcnZlck5hbWUgTVlfTE9DQUxfSVAKICAgIERvY3VtZW50Um9vdCAvdXNyL2xvY2FsL2VsaXhpci9odHRwCiAgICBXU0dJU2NyaXB0QWxpYXMgL2FwaSAvdXNyL2xvY2FsL2VsaXhpci9hcGkvYXBpLnB5CiAgICBBbGxvd0VuY29kZWRTbGFzaGVzIE9uCiAgICBSZXdyaXRlRW5naW5lIG9uCiAgICBSZXdyaXRlUnVsZSAiXi8kIiAiL2Jsa3RyYWNlL2xhdGVzdC9zb3VyY2UiIFtSXQogICAgUmV3cml0ZVJ1bGUgIl4vKD8hYXBpfGFjcCkuKi8oc291cmNlfGlkZW50fHNlYXJjaCkiICIvd2ViLnB5IiBbUFRdCiAgICBSZXdyaXRlUnVsZSAiXi9hY3AiICIvYXV0b2NvbXBsZXRlLnB5IiBbUFRdCjwvVmlydHVhbEhvc3Q+Cg== | base64 -d > /etc/httpd/conf.d/000-elixir.conf \
&& echo -e "\nHttpProtocolOptions Unsafe" >> /etc/httpd/conf/httpd.conf

EXPOSE 80

ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
