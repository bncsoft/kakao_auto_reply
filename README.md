﻿# Kakaotalk Auto Reply

카카오톡에서 제공하는 플러스 친구 / 옐로 아이디 자동 응답 API를 기반으로 만들어진 프로젝트입니다. PHP와 Apache 환경에서 동작하며, PHP 5.3과 PHP 5.5 버전에 대해 테스트하였습니다.<br>
서버에서 가볍게 돌아가는 것을 목표로 하기 때문에 PHP 라이브러리를 사용하지 않았으며 관리자 페이지 디자인의 경우에도 간단하게 구성하였습니다.

## 1. 시스템 요구 사양
PHP 버전은 5.3 이상이어야 하고, Apache에서 mod_rewrite 모듈이 있어야 합니다.<br>
버전이나 모듈에 대한 내용은 호스팅사에 문의하면 알 수 있습니다.

## 2. 세팅 과정
1. 파일을 모두 다운로드 받습니다. (위쪽에 clone or download 버튼을 누르셔서 압축 파일로 다운로드 받으실 수 있습니다.)
1. `config.php` 파일을 열어서 `define("BASE_URL", "");` 항목을 자신에게 맞는 URL를 넣어주시면 됩니다. 참고로 입력할 URL은 `/`로 끝이 끝나야 합니다.<br>
즉, `http://example.com/`나 `http://example.com/auto_reply/`처럼 설정을 하셔야 합니다.
1. 만약 서브 폴더로 운영을 할 경우에는 `.htaccess` 파일을 여신 후 `RewriteRule ^(.*)$ /index.php/?id=$1 [L]` 부분을 자신의 설정에 맞게 변경하셔야 합니다.<br>
`auto_reply`라는 서브 폴더로 운영을 할 경우, `RewriteRule ^(.*)$ /auto_reply/index.php/?id=$1 [L]`로 수정을 하시면 됩니다.
1. 모든 파일을 서버에 올리시면 됩니다.
1. 업로드한 위치로 접속합니다. (2.2의 과정에서 설정했던 `BASE_URL`로 접속을 하시면 됩니다.)
1. 주어진 내용대로 따라가시면 세팅이 끝납니다.
1. 마지막으로 옐로 아이디 관리자 페이지로 가셔서 URL 설정을 2.2의 과정에서 설정했던 `BASE_URL`로 설정하시면 됩니다.

## 3. 중요 파일 및 폴더에 대한 설명
### 3.1 /class
여기에서 사용하는 모든 클래스에 대한 정의를 해놓은 폴더입니다.
### 3.2 /resource
자동 응답에 사용할 데이터를 담고 있는 폴더입니다. 이미지는 `img` 폴더에 저장하며, 텍스트 응답은 `msg` 폴더에서 `php`파일 형식으로 저장합니다. `msg`의 경우에는 직접 접근을 막기 위해서 파일명을 해시처리를 해서 사용합니다.
### 3.3 admin.config.php
관리자 계정에 대한 정보를 담고 있습니다.
### 3.4 config.php
`BASE_URL`의 경우에는 자신의 환경에 맞게 설정을 해주셔야 합니다. 그렇지 않으면 제대로 동작을 할 수 없습니다.<br>
`IP_CHECK`의 경우에는 [카카오톡 IP](https://github.com/plusfriend/auto_reply#71-proxy-server-information)와 테스트를 하는 경우 이외의 IP가 접속했을 때 응답을 보여줄지 말지를 결정하는 것입니다. 보안 상 `TRUE`로 설정을 해놓는 것을 추천합니다.
### 3.5 keyboard.config.php
[Home Keyboard](https://github.com/plusfriend/auto_reply#51-home-keyboard-api)에서 보여줄 키보드 정보를 담고 있습니다.
### 3.6 lib.add.php
사용자가 필요에 의해 재정의를 할 수 있는 부분입니다. 아래는 재정의 할 수 있는 내용입니다.

1. 메시지를 수신해서 처리하기 전에 동작하는 부분 (`pre_message_receive`)
1. 메시지 응답을 보내고 동작하는 부분 (`post_message_receive`)
1. 사용자가 친구추가되었을 때 동작할 부분 (`add_friend`)
1. 사용자가 친구 차단을 했을 때 동작할 부분 (`delete_friend`)
1. 사용자가 채팅방을 나갔을 때 동작할 부분 (`delete_chat_room`)
1. 미디어 파일을 업로드 했을 때 보여줄 메시지 (`msg_media_upload`)
1. 정의되지 않은 메시지가 왔을 때 보여줄 메시지 (`undefined_msg_operation`)

## 4. 기타사항
1. 이 프로젝트는 간단한 응답 봇을 구축하기 위해서 만들어진 것입니다. 즉 여기에 나온대로만 진행하신다면 정적인 응답만 할 수 있습니다. 하지만 응답 파일을 수정해서 현재 날씨를 알려주는 것과 같이 동적인 응답을 하게 할 수 있습니다.
1. 관리자 아이디와 비밀번호가 파일로 저장되고, 암호화를 하지 않기 때문에 파일이 유출되지 않도록 주의하시기 바랍니다.
1. 데이터베이스를 사용하지 않고 모든 내용을 파일로 저장하고 있습니다.
1. 관리자로 접속을 하는 경우 웹 페이지에서 테스트를 직접 수행할 수 있습니다. 다만 주관식으로 입력받는 부분은 구현되지 않고, 객관식으로 입력받는 부분만 구현되었습니다.

## 5. 문의사항
프로젝트에 대한 문의는 이 저장소의 [issue](https://github.com/humit0/kakao_auto_reply/issues)를 이용해주시면 됩니다. 카카오톡 서버에 대한 문의는 여기서 처리할 수 없습니다.

## 6. License
이 프로젝트는 GPLv3 License를 따릅니다.