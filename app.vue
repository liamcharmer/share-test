<script setup>
async function shareVideo() {
  // Web Share API is supported
  const response = await fetch(
    'https://createyourzenspaces.ams3.digitaloceanspaces.com/holiday-vacation-resort-resort-640_Zqu9ctP6.mp4'
  );
  const blob = await response.blob();
  const filesArray = [
    new File([blob], 'video.mp4', {
      type: 'video/mp4',
      lastModified: new Date().getTime(),
    }),
  ];
  const shareData = {
    files: filesArray,
  };
  console.log(shareData);
  console.log(navigator.canShare);
  console.log(navigator.share);
  if (navigator.canShare && navigator.canShare(shareData)) {
    navigator.share(shareData);
  } else {
    // Fallback
    alert('Does not support Web share');
  }
}
</script>
<template>
  <div>
    <p>Hello</p>
    <video
      width="300px"
      height="300px"
      src="https://createyourzenspaces.ams3.digitaloceanspaces.com/holiday-vacation-resort-resort-640_Zqu9ctP6.mp4"
      controls
    />
    <br> <button @click="shareVideo">Share the video</button>
  </div>
</template>
