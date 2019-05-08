<template>
  <div class="modal-cover" v-show="modal" @click="$emit('close-modal')">
    <div class="modal" @click.stop>
      <div class="modal-header">
        <slot name="header"></slot>
      </div>
      <slot>{{modalMsg}}</slot>
      <div class="modal-footer">
        <slot name="footer">
          <button class="close-btn" @click="$emit('close-modal')">Ok</button>
        </slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    modal: {
      type: Boolean,
      default: false
    },
    modalMsg: {
      type: String,
    }
  },
  methods: {
   
  }

}
</script>


<style scoped>
  .modal-cover {
    background: rgba(0, 0, 0, 0.5);
    width: 100%;
    position: absolute;
    top: 0;
    height: 100%;
    z-index: 2;
  }

  .modal {
    width: 430px;
    height: 210px;
    position: absolute;
    top: 45%;
    left: 50%;
    transform: translate(-50%, -50%);
    border: 1px solid grey;
    background: white;
    border-radius: 16px;
    z-index: 3;
    box-shadow: 4px 4px 4px 4px #666;
    font-size: 32px;
    line-height: 100px;
  }
  .modal-header {
    border-bottom: 1px solid grey;
    margin-bottom: 8px;
    border-radius: 16px;
    border-bottom-left-radius: 0px;
    border-bottom-right-radius: 0px;
    width: 100%;
    height:50px;
    background: blue;
  }
  .modal-footer {
    margin-top: -35px;
  }
  .close-btn {
    width:100px;
  }
</style>
