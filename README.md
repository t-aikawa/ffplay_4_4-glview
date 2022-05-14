# ffplay 4.4 on glview


ffmpeg 4.4 のffplay をglview(Opengl-based GUI toolkit for the Wayland display system)で動作するようにポーティングしました。

- 音声出力はSDL2をそのまま使用しています。
- 描画は、ソース修正を少なくする為、SDL2のAPIに合わせてOpenGLで実装しています。


## 開発環境

- OS ：ubuntu 21.10、ビルドシステム：meson
- OpenGL: OpenGL/ES 2.0 Mesa 22.0.1 , OpenGL 4.1(Compatibility Profile) Mesa 22.0.1
- ffmpeg 4.4.1
- glview: version 0.1.18 or later

## 問い合わせ等は、以下のメールアドレスまで

```
aikawat@jcom.home.ne.jp
```

## ビルド手順

```bash
sudo apt install gcc
sudo apt install g++
sudo apt-get install libglib2.0*
sudo apt-get install libway*
sudo apt-get install wayland-protocols
sudo apt-get install libegl1-mesa libegl1-mesa-dev
sudo apt-get install libgles2-mesa-dev
sudo apt-get install libfreetype6-dev
sudo apt-get install libxkbcommon-dev
sudo apt-get install ibus-1.0
sudo apt-get install fcitx-libs-dev
sudo apt-get install libpng-dev
sudo apt-get install fonts-ipa*

sudo apt-get install ninja-build
sudo apt-get install meson

git clone https://github.com/t-aikawa/glview.git
cd glview
chmod +x m mm simple-egl smoke test s001 s002
# コンパイル
./m
# ./m 又は ./m gles で、OpenGL/ES(libGLESv2.so)とリンクします。
# ./m opengl で、OpenGL(libOpenGL.so)とリンクします。
---------------------------------------------------------------------

sudo apt-get install libavcodec-dev
sudo apt-get install libavformat-dev
sudo apt-get install libavfilter-dev
sudo apt-get install libavdevice-dev
sudo apt-get install -y libsdl2-dev libsdl2-image-dev libsdl2-mixer-dev libsdl2-net-dev libsdl2-ttf-dev

cd ../
git clone https://github.com/t-aikawa/ffplay_4_4-glview.git
cd ffplay_4_4-glview
chmod +x m mm
# コンパイル
./m
# ./m 又は ./m gles で、OpenGL/ES(libGLESv2.so)とリンクします。
# ./m opengl で、OpenGL(libOpenGL.so)とリンクします。
# glviewと同じOpenGLを指定してください。
# 再コンパイルのみの場合は、以下を実行してください。
./mm

./builddir/ffplay -i ~/xxxxx.mp4
```
