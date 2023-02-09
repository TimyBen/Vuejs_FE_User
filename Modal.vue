<template>
    <transition>
    <div class="m-out" id="m-out" v-show="open">
        <div class='m-in'>
            <!-- <div class="modal-content"> -->
            <v-btn class="close-icon" @click="$emit('close')">
                <div class="icon"><img src="/xmark-solid.svg"/>
                </div>
            </v-btn>
            <!-- </div> -->
            <div>
                <slot/>
            </div>
            <div class="close_box">
                <div class="close" @click="$emit('close')">
                    <v-btn class="close_button">
                        Close
                    </v-btn>
                </div>
            </div>
        </div>
  </div>
  </transition>
</template>

<script>
export default {
  name: 'ModalComponent',
  props: {
    open: {
      type: Boolean,
      required: true
    }
  }
}
</script>

<style>
.m-out {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0px;
    transition:all 0.5s;
    background: rgba(0, 0, 0, 0.49);
    /* opacity: 0.45; */
}
.m-in {
    position: absolute;
    background-color: white;
    bottom: 0;
    width: 100%;
    border-radius: 10px 10px 0px 0px;
    padding-bottom: 10px;
}
.modal-content {
    /* position: absolute; */
    height: 60px;
}

.close-icon {
    /* position: absolute; */
    width: 15px;
    height: 15px;
    left: 15px;
    top: 15px;

}
.close_box {
    /* position: relative; */
    bottom: 0%;
    padding-left: 5%;
    padding-right: 5%;
    padding-top: 5%;
}

.close {
    /* position: absolute; */
    justify-content: center;
    align-items: center;
    display: flex;
    /* padding: 14px 16px; */
    height: 51px;
    background: #FE5F00;
    border-radius: 4px;
    left: 20px;
}
.close_button {
    text-align: center;
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 24px;
    align-items: center;
    color: #FFFFFF;
    flex: none;
    order: 0;
    flex-grow: 1;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: -1;
}

</style>
