
<script>
export default {
  onLaunch: function() {
    console.log('App Launch');
  }
}
</script>

<style>
/* 引入 Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Epilogue:wght@400;700;900&family=Noto+Serif+SC:wght@700&family=Material+Symbols+Outlined:wght,FILL@300,0..1&display=swap');

page {
  background-color: #f5f3f0;
  font-family: 'Epilogue', 'Noto Sans SC', sans-serif;
  color: #111817;
  -webkit-font-smoothing: antialiased;
}

.editorial-shadow {
  box-shadow: 0 10px 40px -10px rgba(0,0,0,0.08);
}

.font-serif {
  font-family: 'Noto Serif SC', serif;
}

/* Material Symbols 辅助类 */
.material-symbols-outlined {
  font-family: 'Material Symbols Outlined';
  font-weight: normal;
  font-style: normal;
  font-size: 24px;
  line-height: 1;
  letter-spacing: normal;
  text-transform: none;
  display: inline-block;
  white-space: nowrap;
  word-wrap: normal;
  direction: ltr;
  -webkit-font-feature-settings: 'liga';
  -webkit-font-smoothing: antialiased;
}

.material-symbols-outlined.filled {
  font-variation-settings: 'FILL' 1;
}

.no-scrollbar::-webkit-scrollbar {
  display: none;
}
</style>
