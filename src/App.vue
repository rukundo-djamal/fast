<template>
  <v-app id="inspire">
    <v-navigation-drawer fixed :clipped="$vuetify.breakpoint.mdAndUp" app v-model="drawer">
      <template>
        <v-card class="mx-auto" color="#26c6da" dark max-width="400">
          <v-card-title>
            <v-icon large left>mdi-twitter</v-icon>
          </v-card-title>

          <v-card-actions>
            <v-list-tile class="grow">
              <v-icon x-large left dark>account_circle</v-icon>
              <v-list-tile-content>
                <v-list-tile-title>Evan You</v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-card-actions>
        </v-card>
      </template>
      <v-list dense>
        <template v-for="item in items">
          <v-list-group
            v-if="item.children"
            v-model="item.model"
            :key="item.text"
            :prepend-icon="item.model ? item.icon : item['icon-alt']"
            append-icon
          >
            <v-list-tile slot="activator">
              <v-list-tile-content>
                <v-list-tile-title>{{ item.text }}</v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
            <v-list-tile v-for="(child, i) in item.children" :key="i">
              <v-list-tile-action v-if="child.icon">
                <v-icon>{{ child.icon }}</v-icon>
              </v-list-tile-action>
              <v-list-tile-content>
                <v-list-tile-title>{{ child.text }}</v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-list-group>
          <v-list-tile v-else :key="item.text">
            <v-list-tile-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>{{ item.text }}</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </template>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar color="blue darken-3" dark app :clipped-left="$vuetify.breakpoint.mdAndUp" fixed>
      <v-toolbar-title style="width: 300px" class="ml-0 pl-3">
        <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
        <span class="hidden-sm-and-down">Fast</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>vpn_key</v-icon>
      </v-btn>
    </v-toolbar>
    <v-content>
      <hello-world></hello-world>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",
  components: {
    HelloWorld
  },
  data() {
    return {
      dialog: false,
      drawer: null,
      items: [
        { icon: "dashboard", text: "Dashboard" },
        {
          icon: "keyboard_arrow_up",
          "icon-alt": "keyboard_arrow_down",
          text: "Purchase Order",
          model: false,
          children: [
            { icon: "add", text: "Create Purchase order" },
            { icon: "more", text: "more" }
          ]
        },
        {
          icon: "keyboard_arrow_up",
          "icon-alt": "keyboard_arrow_down",
          text: "Invoice",
          model: false,
          children: [
            { icon: "add", text: "Create Invoice" },
            { icon: "more", text: "more" }
          ]
        },
        {
          icon: "keyboard_arrow_up",
          "icon-alt": "keyboard_arrow_down",
          text: "Payment",
          model: false,
          children: [
            { icon: "add", text: "Create Payment" },
            { icon: "more", text: "more" }
          ]
        },
        { icon: "settings", text: "Settings" },

      ]
    };
  }
};
</script>
