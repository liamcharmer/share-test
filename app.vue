<script setup>
let sharingVideo = false;
async function shareVideo() {
  // Web Share API is supported
  sharingVideo = true;
  const response = await fetch(
    'https://createyourzenspaces.ams3.digitaloceanspaces.com/holiday-vacation-resort-resort-640_Zqu9ctP6.mp4'
  );
  const blob = await response.blob();
  sharingVideo = false;
  const filesArray = [
    new File([blob], 'video.mp4', {
      type: 'video/mp4',
      lastModified: new Date().getTime(),
    }),
  ];
  const shareData = {
    files: filesArray,
    title: 'Title here',
    text: 'This is some text that can be provided',
  };
  console.log(shareData);
  console.log(navigator.canShare);
  console.log(navigator.share);
  if (navigator.canShare && navigator.canShare(shareData)) {
    navigator.share(shareData);
  } else {
    // Fallback
    window
      .open(
        'https://createyourzenspaces.ams3.digitaloceanspaces.com/holiday-vacation-resort-resort-640_Zqu9ctP6.mp4',
        '_blank'
      )
      .focus();
  }
}
</script>
<template>
  <div>
    <p>Hello</p>
    <video
      autoplay
      loop
      muted
      playsinline
      width="300px"
      height="300px"
      src="https://createyourzenspaces.ams3.digitaloceanspaces.com/holiday-vacation-resort-resort-640_Zqu9ctP6.mp4"
      controls
    />
    <br> <button @click="shareVideo">Share the video</button>
    {{sharingVideo}}
    <p v-if="sharingVideo">Downloading video for share usage...</p>
  </div>
</template>
