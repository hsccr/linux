glib-config, gtk-config 등의 *-config script는 오래전에 compiler, linker의 flag들을 설정하기 위한 것이었습니다. 그런데, GTK+-2.0대로 넘어오면서 이 *-config script들을 통합한 pkg-config라는 프로그램이 등장합니다. pkg-config는 대개 설정 파일들을 /usr/lib/pkgconfig/에서 읽어옵니다. 만약 설정 파일이 다른 곳에 위치해 있다면 환경 변수인 PKG_CONFIG_PATH를 그 위치로 지정해 주어야 합니다. GTK+ 2.0 등을 source에서 설치하셨다면 default로 /usr/local/lib/pkgconfig/에 관련 설정 파일이 쌓일 테니, 다음과 같이 설정하면 됩니다:

export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig:/usr/lib/pkgconfig
참고로 위 환경 변수 내용을 바꾸기 전에 pkg-config를 실행해서, pkg-config가 제대로 설정 파일을 인식했는지 확인할 수도 있습니다:

$ pkg-config --list-all

To do this in a distro-independent* fashion you can use ldconfig with grep, like this:
ldconfig -p | grep libjpeg

pacman -S protobuf

pacman -S webkitgtk

pacman -S libmicrohttpd

pacman -S protobuf-c

pacman -S libuv
