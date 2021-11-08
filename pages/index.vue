<template>
  <Tutorial/>
</template>

<script lang="ts">
import Vue from 'vue';
import createApp from '@shopify/app-bridge';
import { Redirect } from '@shopify/app-bridge/actions';

const apiKey = '4f11a728f162984ae3ad533cb848bf4a';
const redirectUri = 'https://cb-shopify-nuxt.netlify.app/';
const host1 = "cb-revs-store.myshopify.com";
const permissionUrl = `https://${host1}/admin/oauth/authorize?client_id=${apiKey}&scope=read_products,read_content&redirect_uri=${redirectUri}`;

export default Vue.extend({})
if (window.top == window.self) {
  window.location.assign(permissionUrl);

  // If the current window is the 'child', change the parent's URL with Shopify App Bridge's Redirect action
} else {
  const app = createApp({
    apiKey: apiKey,
    host: host1
  });

  Redirect.create(app).dispatch(Redirect.Action.REMOTE, permissionUrl);
  
}
</script>
