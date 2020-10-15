<template>
  <div class="footer">
  <p>
    Copyright©2020
    &nbsp;
    <a href="//nana-movie.top" target="_blank" title="娜微原创" rel="nofollow" class="footer-record">娜微原创</a>
    &nbsp;
    <img src="@/static/img/beian.png" class="footer-icom"/>
    <a href="http://www.beian.miit.gov.cn/" target="_blank" rel="nofollow" class="footer-record">
    湘ICP备20002747号-1</a>
    &nbsp;
    </p>
  </div>
</template>

<script>
export default {
  inheritAttrs: false,
  name: 'myFooter'
}
</script>

<style>
.footer {
  position: relative;
  bottom: 0;
  width: 100vw;
  font-size: 0.3467rem;
  text-align: center;
  vertical-align: middle;
  color: #999;
  background-color: transparent;
}
.footer-icom {
  display: inline-block;
  width: 0.48rem;
  height: auto;
  margin-top: -4px;
  background-size: cover;
  vertical-align: middle;
}
.footer-record {
  color: #999;
  font-size: 0.3467rem; 
}
a:hover {
 text-decoration: underline;
}
</style>