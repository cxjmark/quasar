<template>
  <div class="q-layout-padding row justify-center" style="width: 500px; max-width: 90vw;">
    <div class="fixed-center z-max">
      <div class="row group">
        <div>
          <q-btn round size="sm" color="secondary" @click="alertAsMethod('top-left')">
            <q-icon name="arrow_back" class="rotate-45" />
          </q-btn>
        </div>
        <div>
          <q-btn round size="sm" color="accent" @click="alertAsMethod('top')">
            <q-icon name="arrow_upward" />
          </q-btn>
        </div>
        <div>
          <q-btn round size="sm" color="secondary" @click="alertAsMethod('top-right')">
            <q-icon name="arrow_upward" class="rotate-45" />
          </q-btn>
        </div>
      </div>
      <div class="row group">
        <div>
          <q-btn round size="sm" color="accent" @click="alertAsMethod('left')">
            <q-icon name="arrow_back" />
          </q-btn>
        </div>
        <div>
          <q-btn round size="sm" color="accent" @click="alertAsMethod('center')">
            <q-icon name="fullscreen_exit" />
          </q-btn>
        </div>
        <div>
          <q-btn round size="sm" color="accent" @click="alertAsMethod('right')">
            <q-icon name="arrow_forward" />
          </q-btn>
        </div>
      </div>
      <div class="row group">
        <div>
          <q-btn round size="sm" color="secondary" @click="alertAsMethod('bottom-left')">
            <q-icon name="arrow_forward" class="rotate-135" />
          </q-btn>
        </div>
        <div>
          <q-btn round size="sm" color="accent" @click="alertAsMethod('bottom')">
            <q-icon name="arrow_downward" />
          </q-btn>
        </div>
        <div>
          <q-btn round size="sm" color="secondary" @click="alertAsMethod('bottom-right')">
            <q-icon name="arrow_forward" class="rotate-45" />
          </q-btn>
        </div>
      </div>
    </div>

    <q-btn round icon="touch_app" @click="showGroup1" color="primary" class="absolute-top-left" />
    <q-btn round icon="touch_app" @click="showGroup2" color="secondary" class="absolute-bottom-left" />
  </div>
</template>

<script>
const alerts = [
  { color: 'negative', message: 'Woah! Danger! You are getting good at this!', icon: 'report_problem' },
  { message: 'You need to know about this!', icon: 'warning' },
  { message: 'Wow! Nice job!', icon: 'thumb_up' },
  { color: 'teal', message: 'Quasar is cool! Right?', icon: 'tag_faces' },
  { color: 'purple', message: 'Jim just pinged you', avatar: 'https://cdn.quasar.dev/img/boy-avatar.png' },
  { multiLine: true, message: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Hic quisquam non ad sit assumenda consequuntur esse inventore officia. Corrupti reiciendis impedit vel, fugit odit quisquam quae porro exercitationem eveniet quasi.' }
]

export default {
  data () {
    return {
      visible: true,
      visible2: true
    }
  },
  methods: {
    showGroup1 () {
      this.$q.notify({
        message: 'Grouped message ' + Math.random(),
        group: 'some-group',
        progress: true,
        badgeColor: 'teal'
      })
    },

    showGroup2 () {
      this.$q.notify({
        message: 'Some message',
        progress: true
      })
    },

    alertAsMethod (position) {
      const { color, textColor, multiLine, icon, message, avatar } = alerts[ Math.floor(Math.random(alerts.length) * 10) % alerts.length ]
      const random = Math.random() * 100

      const twoActions = random > 70
      const buttonColor = color ? 'white' : void 0

      this.$q.notify({
        color,
        textColor,
        icon: random > 30 ? icon : null,
        message,
        caption: random < 30 ? '5 minutes ago' : null,
        position,
        avatar,
        multiLine,
        progress: true,
        actions: twoActions
          ? [
            { label: 'Reply', color: buttonColor, handler: () => console.log('wooow') },
            { label: 'Dismiss', color: 'yellow', handler: () => console.log('wooow') }
          ]
          : (random > 40
            ? [ { label: 'Reply', color: buttonColor, handler: () => console.log('wooow') } ]
            : null
          ),
        timeout: Math.random() * 5000 + 3000
      })
      /* closeBtn test
      this.$q.notify({
        color,
        textColor,
        icon,
        message,
        position,
        avatar,
        closeBtn: true,
        actions: Math.random() * 100 > 50
          ? [ { label: 'Reply', handler: () => console.log('wooow') } ]
          : null,
        timeout: Math.random() * 5000 + 3000
      })
      */
    }
  },

  mounted () {
    this.$q.notify.setDefaults({
      color: 'red'
    })
    this.$q.notify('red; with defaults')
    this.$q.notify({
      message: 'discarded defaults',
      ignoreDefaults: true
    })
    this.$q.notify.setDefaults({
      color: void 0
    })

    this.$q.notify({
      message: '<em>I can</em> <span style="color: red">inject</span> <strong>HTML</strong>',
      html: true
    })
    /*
    this.$q.notify.setDefaults({
      actions: [{ icon: 'close', handler () { console.log('cloooose') } }]
    })
    */
    this.$q.notify({
      message: 'You need to know about this!',
      caption: 'This is a caption',
      timeout: 0,
      avatar: 'https://cdn.quasar.dev/img/boy-avatar.png'
    })
    this.$q.notify({
      message: 'You need to know about this!',
      caption: 'This is a caption',
      timeout: 0,
      color: 'yellow',
      textColor: 'black',
      multiLine: true,
      avatar: 'https://cdn.quasar.dev/img/boy-avatar.png',
      actions: [ { label: 'Reply', handler: () => console.log('wooow') } ]
    })
    this.$q.notify({
      html: true,
      icon: 'map',
      avatar: 'https://cdn.quasar.dev/img/boy-avatar.png',
      message: 'HTML; You need to know about this!',
      caption: 'This is a caption',
      timeout: 0
    })
    this.$q.notify({
      html: true,
      message: 'HTML; You need to know about this!',
      caption: 'This is a caption',
      timeout: 0,
      closeBtn: 'Close',
      color: 'yellow',
      textColor: 'black',
      multiLine: true,
      avatar: 'https://cdn.quasar.dev/img/boy-avatar.png',
      actions: [ { label: 'Reply', handler: () => console.log('wooow') } ]
    })
  }
}
</script>
