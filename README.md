# Orange-Chat-Notifier
Cuz Orange.eg support chat has no tune.

## The problem:
When you chat with support you will have to wait upto almost 25min before a rep reply to you.
you will be surfing on other tabs and will not notice if a message is recived and the chat will end automatically.

## My solution:
If you chatting from the desktop then all you need is to open the inspector (ctrl + shift + T) then choose the Console tab.
Paste the follwing code, hit Enter and it will do two things:
1. make a sound when the chat message is recieved or sent.
2. change the avatar to an actual orange instead of the [hitler avatar](https://livechat.orange.eg/chat/images/agent.png) .

Note this was tested only on chrome.
```javascript
var notification_beep_url = "https://upload.wikimedia.org/wikipedia/commons/d/df/Chord2_%21_%28Ab-C-D-G%29.mp3";
var notification_beep = new Audio(notification_beep_url);
var orange_avatar = "https://upload.wikimedia.org/wikipedia/commons/d/dc/Orange-fruit.png";

var chatCount = function(){
	return document.querySelectorAll('.chat li').length;
}

var get_chat_count = function(){
	return document.querySelectorAll('.chat li').length;
}
var current_chat_count = get_chat_count();
var updated_chat_count = get_chat_count();

function orangeChatAvatarToAnOrange(){
	var chat_image = document.querySelectorAll('.chat-img');
	chat_image[updated_chat_count - 2].style.backgroundImage = "url("+orange_avatar+")";
	chat_image[updated_chat_count - 2].style.backgroundRepeat = "no-repeat";
	chat_image[updated_chat_count - 2].style.backgroundSize = "40px 40px";
	chat_image[updated_chat_count - 2].style.backgroundPosition = "center";
	chat_image[updated_chat_count - 2].style.width = "50px";
	chat_image[updated_chat_count - 2].style.height = "50px";

	chat_image[updated_chat_count - 2].querySelector('img').style.display = 'none';
}

function orangeChatNotification(){
	if(chatCount != 0){
		updated_chat_count = get_chat_count();

		if( (current_chat_count != updated_chat_count) && (current_chat_count > 0) ){

			notification_beep.play()
			current_chat_count = updated_chat_count;

			orangeChatAvatarToAnOrange();
		}
	}
}


setInterval(orangeChatNotification, 300);
```
