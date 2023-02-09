<template>
    <transition>
        <div class="m-out" v-show="open">
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
                <div class="feedback">
                    <div class="btn_feedback">
                        <router-link class="btn_feedback_txt" to="/FeedBack">
                            Feed Back
                        </router-link>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
export default {
  name: 'RewardInfoModal',
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
    position: absolute;
    width: 15px;
    height: 15px;
    left: 15px;
    top: 15px;

}
.feedback {
    bottom: 0%;
    padding-left: 5%;
    padding-right: 5%;
    padding-top: 5%;
}

.btn_feedback {
    justify-content: center;
    align-items: center;
    display: flex;
    height: 51px;
    background: #E6E9EC;
    border-radius: 4px;
}
.btn_feedback_txt {
    text-decoration: none;
    text-align: center;
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 24px;
    align-items: center;
    color: #072553;
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
