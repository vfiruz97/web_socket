# websocket_universal_x
**Note**: `Not recommended to use.`

This code was forked from [websocket_universal](https://pub.dev/packages/websocket_universal) Dart/Flutter package. In this project `the lib/http` folder was cloned from `Dart SDK` accordingly and changed due to this [GitHub issue response](https://github.com/dart-lang/sdk/issues/55810#issuecomment-2137140851). And also did replaced `the http from SDK` with customised `lib/http` in some `websocket_universal` files. All this because the hand-coded backend at work which fails to receive frame from Dart WebSocket Client.

## TAG
 - last tag: 1.0.1

 ```bash
  git commit -m 'comment-name'
  git push origin master

  git tag 1.0.1
  git push --tags
 ```

## Flutter
 ```yaml
 dependencies:
  websocket_universal_x:
    git:
      url: git@github.com:vfiruz97/web_socket.git
      ref: 1.0.0

 ```

 ## Example

 ```bash
 import 'dart:io';

import 'package:websocket_universal_x/websocket_universal.dart';

void main() async {
  const params = SocketOptionalParams(headers: {});

  final textSocketHandler = IWebSocketHandler<String, String>.createClient(
    wssServerUrl,
    SocketSimpleTextProcessor(),
    connectionOptions: const SocketConnectionOptions(),
  );

  textSocketHandler.logEventStream.listen((event) {
    print('> webSocket error: "${event.socketLogEventType}", "${event.data}",'
        ' "${event.message}", "${event.status}"');
  });

  await textSocketHandler.connect(
    params: params,
  );

  textSocketHandler.sendMessage('data');
  await Future.delayed(const Duration(milliseconds: 300));

  for (int i = 0; i < 30; i++) {
    textSocketHandler.sendMessage('data $i');
    await Future.delayed(const Duration(milliseconds: 100));
  }

  textSocketHandler.close();
  exit(0);
}
 ```


