<template>
  <b-list-group class="listGroup thin-scroll">
    <b-list-group-item class="listGroupItem">
      <span class="notificationIcon thumb-sm">
        <!-- <img class="rounded-circle" src="../../../assets/people/a3.jpg" alt="..." /> -->
      </span>
      <p class="m-0 overflow-hidden">
        Water Pump was activated in response to low moisture levels
        <time class="help-block m-0">
          1 hour ago
        </time>
      </p>
    </b-list-group-item>
    <b-list-group-item class="listGroupItem">
      <span class="notificationIcon thumb-sm">
        <!-- <i class="fa fa-angle-double-up fa-2x" /> -->
      </span>
      <p class="text-ellipsis m-0">
        New firmware update for Motion Sensors is here, press the update button on the device to continue
        <time class="help-block m-0">
          5h ago
        </time>
      </p>
    </b-list-group-item>
  </b-list-group>
</template>

<script>
export default {
  name: 'NotificationsList',
};
</script>

<style src="./ListGroup.scss" lang="scss" />
