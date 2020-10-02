<template>
  <q-item clickable v-ripple exact :to="to">
    <q-item-section avatar>
      <q-icon :color="color" :name="icon" />
    </q-item-section>

    <q-item-section>{{ title }}</q-item-section>
  </q-item>
</template>

<script>
export default {
  name: 'EssentialLink',
  props: [
    'title', 'to', 'icon'
  ],
  data () {
    return {
      color: ''
    }
  },
  methods: {
    click () {
      this.color = 'primary'
    }
  }
}
</script>
