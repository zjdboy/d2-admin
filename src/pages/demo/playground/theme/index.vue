<template>
  <d2-container type="full" class="page">
    <template slot="header">主题</template>
    <el-table :data="themeList" v-bind="table">
      <el-table-column prop="name" align="center" width="260"/>
      <el-table-column label="预览" width="120">
        <div
          slot-scope="scope"
          class="theme-preview"
          :style="{'backgroundImage': `url(${$assetsPublicPath}${scope.row.preview})`}">
        </div>
      </el-table-column>
      <el-table-column prop="address" align="center">
        <template slot-scope="scope">
          <el-button v-if="themeActiveName === scope.row.name" type="success" icon="el-icon-check" round>已激活</el-button>
          <el-button v-else round @click="handleSelectTheme(scope.row.name)">使用</el-button>
        </template>
      </el-table-column>
    </el-table>
    <div>
      <p>尝试激活一个不存在的主题（主题不存在 <d2-icon name="arrow-right"/> 默认主题）</p>
      <el-button type="danger" @click="handleSelectTheme('err-theme')">
        <d2-icon name="hand-o-right" class="d2-mr-10"/>
        尝试激活主题 'err-theme'
      </el-button>
    </div>
    <template slot="footer">
      <el-button type="primary" size="small">当前激活主题 {{themeActiveName}}</el-button>
    </template>
  </d2-container>
</template>

<script>
import { mapState, mapMutations } from 'vuex'
export default {
  data () {
    return {
      table: {
        showHeader: false,
        border: true
      }
    }
  },
  computed: {
    ...mapState({
      themeList: state => state.d2admin.themeList,
      themeActiveName: state => state.d2admin.themeActiveName
    })
  },
  methods: {
    ...mapMutations([
      'd2adminThemeSet'
    ]),
    handleSelectTheme (name) {
      this.d2adminThemeSet(name)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~@/assets/style/public.scss';
.page {
  .theme-preview {
    height: 50px;
    width: 100px;
    border-radius: 4px;
    background-size: cover;
    border: 1px solid $color-border-1;
  }
}
</style>