# 初始化项目 gitee

# unipush
```
//收到透传消息
		//只有APP在线时，才会触发receive事件，透传消息不会触发系统消息,需要创建本地消息
		plus.push.addEventListener(
			'receive',
			function(msg) {
				console.log('(receive):' + JSON.stringify(msg));
				if (app.isIOS()) {
					//如果是IOS
					var payload = msg.payload;
					//【APP在线】收到消息，不会触发系统消息,需要创建本地消息，但不能重复创建。必须加msg.type验证去除死循环
					if (msg.aps == null && msg.type == 'receive') {
						var messageTitle = payload.messageTitle;
						var messageContent = payload.messageTitle;
						//创建本地消息,发送的本地消息也会被receive方法接收到，但没有type属性，且aps是null
						plus.push.createMessage(messageContent, JSON.stringify(payload), { title: messageTitle });
					}
				}
				if (app.isAndroid()) {
					console.log('rec');
					//如果是Android，当APP在线时，收到透传消息不会进入系统消息，需要发送本地提醒。
					// var payload = JSON.parse(msg.payload);
					// var messageTitle = payload.title;
					// var messageContent = payload.content;
					// plus.push.createMessage("content也是不会变得", msg.payload, { title: "固定title" });
				}
			},
			false
		);

		//消息点击事件
		//【APP在线】，收到透传消息通过，不会提醒至通知栏目，需要发送本地消息，再进行点击触发的点击事件。
		//【APP离线】，收到离线透传消息，必须通过Java后台的Intent字符串携带payload，且符合格式才能触发click事件，格式不符合不会触发。
		plus.push.addEventListener(
			'click',
			function(msg) {
				console.log('(click):' + JSON.stringify(msg));
				if (app.isIOS()) {
					//如果是IOS
					var payload;
					if (msg.type == 'click') {
						//APP离线点击包含click属性，这时payload是JSON对象
						payload = msg.payload;
					} else {
						//APP在线，收到消息不会包含type属性,这时的payload是JSON字符串，需要转为JSON对象
						payload = JSON.parse(msg.payload);
					}
					if (payload != null || payload != undefined) {
						var messageType = payload.messageType;
						messageClick(messageType, payload);
					}
				}
				if (app.isAndroid()) {
					//如果是Android，收到playload均是是JSON字符串，需要转为JSON对象
					var payload = JSON.parse(msg.payload);
					if (payload != null || payload != undefined) {
						var messageType = payload.messageType;
						messageClick(messageType, payload);
					}
				}
			},
			false
		);
```
