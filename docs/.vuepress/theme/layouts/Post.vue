<template>
  <div class="post">
    <header-layout></header-layout>
    <div class="post-content">
      <div class="post-title">
        {{ $page.title }}
        <p class="date">
          <span v-if="$page.author">作者: {{ $page.author }}</span>
          <span>发布日期：{{ $page.createdAt }}</span>
          <span v-if="$page.lastUpdated">更新于 {{ $page.lastUpdated | formatDate }}</span>
        </p>
      </div>
      <Content class="content" />
      <div class="post-anchor">
        <a-anchor :offsetTop="100">
          <a-anchor-link class="anchor-item" v-for="(item, index) in $page.headers" :key="index" :href="`#${item.slug}`" :title="item.title" />
        </a-anchor>
      </div>
    </div>
  </div>
</template>

<script>
import HeaderLayout from '../components/Header.vue';

export default {
  components: { HeaderLayout },
  filters: {
    formatDate(value) {
      return new Date(value).toLocaleString();
    },
  },
};
</script>

<style lang="scss" scoped>
.post-content {
  width: 900px;
  margin: 0 auto;
  padding: 40px 0;
  position: relative;
  left: -200px;
  .post-title {
    font-size: 2.2rem;
    font-weight: bold;
    margin-bottom: 30px;
  }
  .date {
    margin: 0;
    font-size: 12px;
    margin-top: 3px;
    color: #c0c0c0;
    span {
      margin-right: 20px;
    }
  }
  .post-anchor {
    position: absolute;
    left: 50%;
    top: 140px;
    margin-left: 450px;
    padding-left: 15px;
    line-height: 30px;
    padding: 10px 15px;
    width: 400px;
    /deep/.ant-anchor-wrapper {
      background-color: #282c35;
      .anchor-item {
        margin-bottom: 5px;
        display: block;
        a {
          color: #c0c0c0;
        }
      }
      .ant-anchor-link-active {
        a {
          color: #fff;
        }
      }
      .ant-anchor-ink::before {
        background-color: #666;
      }
      .ant-anchor-link-title {
        white-space: initial;
      }
    }
  }
}
</style>
