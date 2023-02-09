<template>
    <div class="h">Tỷ lệ chấp nhận đơn hàng</div>
    <div class="note_container">
        <div id="note_box">Giải thích ý nghĩa của tỷ lệ chấp nhận đơn hàng là Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
    </div>
</template>

<script>
export default {
  name: 'PreRequisites',
  data () {
    // return {
    //   isOpen: false,
    //   modalC: 'InfoM'
    // }
  }
//   components: { InfoModal }
}

</script>

<style>
.h {
    padding-top: 5px;
    padding-bottom: 5px;
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 24px;
    text-align: left;
    color: #1A1A1A;
}

.note_container {
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 20px;
    text-align: left;
    color: #4D5358;
}

#note_box {
    white-space: pre-line;
    display: flex;
    /* padding-left: 8px; */
}
</style>
