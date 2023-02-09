<template>
    <!-- <teleport to='#m-out'> -->
    <transition>
    <div class="filter_modal-out" v-show="open">
        <div class='filter_modal-in'>
            <div class="filter_modal-cnt">
            <div>
                <slot/>
            </div>
            <!-- <div class="close_container">
                <div class="close" @click="$emit('close')">
                    <v-btn class="close_button">
                        Tôi đã hiểu
                    </v-btn>
                </div>
            </div> -->
        </div>
        </div>
    </div>
    </transition>
<!-- </teleport> -->
</template>

<script>
export default {
  name: 'InfoModal',
  props: {
    open: {
      type: Boolean,
      required: true
    }
  }
}
</script>

<style>
.filter_modal-out {
    position: absolute;
    width: 100%;
    height: 80%;
    bottom: 0%;
    transition:all 0.5s;
    background: rgba(0, 0, 0, 0.272);
    /* opacity: 0.4; */
    display: flex;
    align-content: center;
    justify-content: center;
}
.filter_modal-in {
    position: absolute;
    width: 100%;
    background: #FFFFFF;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.04);
    border-radius: 4px;
    /* top: 20%; */
}

.filter_modal-cnt {
/* position: absolute; */
}

.close_container {
    /* position: relative; */
    bottom: 0%;
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
