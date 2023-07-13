<template>
	<body>
		<div class="notif-container"></div>
        <div class="notification template"></div>
	</body>
</template>

<script>
//import { reactive } from "vue";
/*export default {
	name: "App",
	setup() {
		const notify = reactive({
			uiEnabled: true,
			voiceModes: [],
			voiceMode: 0,
			radioChannel: 0,
			radioEnabled: true,
			usingRadio: false,
			callInfo: 0,
			talking: false,
		});

		
	}
};*/
	window.addEventListener('message', function (event) {
		switch(event.data.action) {
			default:
				Notify(event.data);
				break;  
		}
	});

	function Notify(data) {
		var $notification = $('.notification.template').clone();
		$notification.removeClass('template');
		$notification.addClass(data.type);
		$notification.html(data.text);
		$notification.fadeIn();
		$('.notif-container').append($notification);
		setTimeout(function() {
			$.when($notification.fadeOut()).done(function() {
				$notification.remove()
			});
		}, data.length === undefined ? data.length : 2500);
	}


</script>

<style>
body {
    background-color: transparent !important;
}

.template, .notification {
    display: none;
}

.notif-container {
    width: 20%;
    position: absolute;
    right: 15%;
    display: flex;
    flex-flow: row;
    flex-wrap: wrap;
}

.notification {
    margin:6px;
    /* text-align:center; */
    font: caption;
    padding:8px;
    border: 2px solid rgba(0, 0, 0, 0.1);
    border-radius:3px;
    font-weight:bold;
    font-size:12px;
    display:inline-block;
}
  

.success {
    background: rgba(104, 189, 123, 0.95);
    color: #fff;
}

.primary {
    background-color: rgba(44, 63, 80, 0.85);
    color: #ffffff;
}

.error {
    background: rgba(181, 82, 85, 0.85);
    color: #fff;
}

</style>
