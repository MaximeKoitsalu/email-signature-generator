<template>
  <v-container class="bg" fluid fill-height>
    <v-layout row wrap justify-center align-center>
      <v-flex xs12 sm5 text-xs-center>
        <h2 class="headline pa-3 grey--text text--lighten-3">Details</h2>
        <v-card>
          <v-card-text>
            <v-container grid-list-md>
              <v-layout row wrap>
                <v-flex xs12>
                  <v-text-field v-model="details.fullName" label="Full Name" @focus="selectedFullName = 1 - selectedFullName" @blur="selectedFullName = 1 - selectedFullName" :append-icon="visibilityFullName ? 'visibility' : 'visibility_off'" @click:append="visibilityFullName = 1 - visibilityFullName"></v-text-field>
                </v-flex>
                <v-flex xs12>
                  <v-text-field v-model="details.position" label="Position" @focus="selectedPosition = 1 - selectedPosition" @blur="selectedPosition = 1 - selectedPosition" :append-icon="visibilityPosition ? 'visibility' : 'visibility_off'" @click:append="visibilityPosition = 1 - visibilityPosition"></v-text-field>
                </v-flex>
                <v-flex xs12>
                  <v-text-field v-model="details.phoneNumber" label="Phone number" @focus="selectedPhoneNumber = 1 - selectedPhoneNumber" @blur="selectedPhoneNumber = 1 - selectedPhoneNumber" :append-icon="visibilityPhoneNumber ? 'visibility' : 'visibility_off'" @click:append="visibilityPhoneNumber = 1 - visibilityPhoneNumber"></v-text-field>
                </v-flex>
                <v-flex xs12>
                  <v-text-field v-model="details.address" label="Address" @focus="selectedAddress = 1 - selectedAddress" @blur="selectedAddress = 1 - selectedAddress" :append-icon="visibilityAddress ? 'visibility' : 'visibility_off'" @click:append="visibilityAddress = 1 - visibilityAddress"></v-text-field>
                </v-flex>
                <v-flex xs12 sm6>
                  <v-text-field v-model="details.logomark" label="Logomark URL" :append-icon="visibilityLogomark ? 'visibility' : 'visibility_off'" @click:append="visibilityLogomark = 1 - visibilityLogomark"></v-text-field>
                </v-flex>
                <v-flex xs12 sm6>
                  <v-text-field v-model="details.logotype" label="Logotype URL" :append-icon="visibilityLogotype ? 'visibility' : 'visibility_off'" @click:append="visibilityLogotype = 1 - visibilityLogotype"></v-text-field>
                </v-flex>
              </v-layout>
            </v-container>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex hidden-xs-only text-xs-center sm2><v-icon x-large class="grey--text text--lighten-3">chevron_right</v-icon></v-flex>
      <v-flex xs12 sm5 text-xs-center>
        <h2 class="headline pa-3 grey--text text--lighten-3">Preview</h2>
        <v-card>
        <v-toolbar class="elevation-3" color="light-blue darken-4" dark>
          <v-btn icon><v-icon>arrow_back</v-icon></v-btn>
          <v-toolbar-title>Compose</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon><v-icon>send</v-icon></v-btn>
        </v-toolbar>
        <v-container fluid class="pa-0 mt-2">
          <v-layout text-xs-left wrap>
            <v-flex xs2>
              <v-subheader>To</v-subheader>
            </v-flex>
            <v-flex xs12 class="text-xs-left">
              <v-chip>
                <v-avatar>
                  <img src="https://randomuser.me/api/portraits/women/16.jpg" >
                </v-avatar>
                Jane Doe
              </v-chip>
              <v-chip>
                <v-avatar>
                  <img src="https://randomuser.me/api/portraits/men/27.jpg" >
                </v-avatar>
                John Smith
              </v-chip>
            </v-flex>
            <v-flex xs12>
              <v-divider></v-divider>
              <v-text-field
                label="Subject"
                value="Plans for the weekend"
                single-line
                full-width
                hide-details
              ></v-text-field>
            </v-flex>
            <v-flex xs12>
              <v-divider></v-divider>
              <v-textarea
                label="Message"
                v-model="message"
                full-width
                hide-details
                auto-grow
                multi-line
                single-line
                class="pa-0"
              ></v-textarea>
              <table cellspacing="0" cellpadding="0" style="padding-left: 12px; margin-top: 15px; margin-bottom: 5px;">
                  <tr>
                    <transition name="slide-y-transition">
                      <td v-show="visibilityLogomark" class="table-border-right">
                        <img
                          :src="details.logomark"
                          style="width: 50px; height: 68px;"
                          height="68"
                          width="50"
                        >
                      </td>
                    </transition>
                    <td>
                      <table cellspacing="0" cellpadding="0">
                      <transition name="slide-y-transition"><tr v-show="details.logotype ^ visibilityLogotype"><div><img style="width: 96px; height: 19px;" height="19" width="96" :src="details.logotype"></div></tr></transition>
                      <transition name="slide-y-transition"><tr v-show="details.fullName ^ visibilityFullName"><div v-bind:class="{ 'primary--text' : selectedFullName}" style="font-weight: bold; line-height: 25px; font-size: 15px;">{{ details.fullName }}</div></tr></transition>
                      <transition name="slide-y-transition"><tr v-show="details.position ^ visibilityPosition"><div v-bind:class="{ 'primary--text' : selectedPosition}" style="line-height: 24px; font-size: 14px;">{{ details.position }}</div></tr></transition>
                      <transition name="slide-y-transition"><tr v-show="details.phoneNumber ^ visibilityPhoneNumber"><div v-bind:class="{ 'primary--text' : selectedPhoneNumber}" style="line-height: 24px; font-size: 14px;">{{ details.phoneNumber }}</div></tr></transition>
                      <transition name="slide-y-transition"><tr v-show="details.address ^ visibilityAddress"><div v-bind:class="{ 'primary--text' : selectedAddress}" style="line-height: 24px; font-size: 14px;">{{ details.address }}</div></tr></transition>
                    </table>
                    </td>
                  </tr>
                </table>
            </v-flex>
          </v-layout>
        </v-container>
      </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      details: {
        fullName: "John Doe",
        phoneNumber: "+46 70 - 123 45 67",
        email: "john.doe@example.com",
        position: "Software Engineer",
        companyName: "John Doe Ltd",
        website: "www.example.com",
        address: "Main Street 1, 123 45, Anytown",
        logotype: 'https://server.app.trovisio.com/static/trovisio-header.png',
        logomark: 'https://server.app.trovisio.com/static/trovisio-logo.png'
      },
      visibilityFullName: 1,
      visibilityPosition: 1,
      visibilityPhoneNumber: 1,
      visibilityAddress: 1,
      visibilityLogotype: 1,
      visibilityLogomark: 1,
      selectedFullName: 0,
      selectedPosition: 0,
      selectedPhoneNumber: 0,
      selectedAddress: 0,
      message:
        "Hi,\n\nI just wanted to check in and see if you had any plans the upcoming weekend. We are thinking of heading up to Napa. \n\nRegards,"
    }
  },
  name: "Email-Signature-Generator"
};
</script>

<style scoped>
.bg {
  background: linear-gradient(90deg, #4b6cb7 0%, #182848 100%);
}

.blue {
  background: blue;
}
</style>
