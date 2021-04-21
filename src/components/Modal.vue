<template>
  <div class="modal-backdrop">
    <div class="modal">
      <header class="modal-header">
        <slot name="header">
          <h3 class="rules-word">RULES</h3>
        </slot>
        <button
          type="button"
          class="btn-close"
          @click="close"
        >
          X
        </button>
      </header>

      <section class="modal-body">
        <slot class="the-body" name="body">
        </slot>
       </section>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Modal',
    methods: {
      close() {
        this.$emit('close');
      },
    },
  };
</script>

<style>
  .modal-backdrop {
    /* background-color: rgba(0, 0, 0, 0.3); */
    width: 50%;
    height: 100%;

  }

  .modal {
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    height:50%;
    flex-direction: column;
    border-radius: 10px;
  }

  .modal-header{
    padding: 15px;
    display: flex;
    background-color: #ffffff;
  }

  .modal-header {
    position: relative;
    color: #3e435f;
    justify-content: space-between;
    height: 20%;
  }

  .modal-footer {
    border-top: 1px solid #eeeeee;
    flex-direction: column;
    justify-content: flex-end;
  }

  .modal-body {
    background-image: url(../assets/desktop-rules-modal-cropped.jpg);
    background-color: #ffffff;
    background-repeat: no-repeat;
    background-position: center;
    position: relative;
    padding: 30px 10px;
    height: 100%;
  }

  .btn-close {
    position: absolute;
    top: 0;
    right: 0;
    border: none;
    font-size: 20px;
    padding: 10px;
    cursor: pointer;
    font-weight: bold;
    color: #4AAE9B;
    background: transparent;
  }

  .btn-green {
    color: white;
    background: #4AAE9B;
    border: 1px solid #4AAE9B;
    border-radius: 2px;
  }
  .the-body{
      height:100%;
  }

  .rules-word{
      position: absolute;
      top: 10%;
      left: 45%;
      font-size: 30px;
  }

</style>