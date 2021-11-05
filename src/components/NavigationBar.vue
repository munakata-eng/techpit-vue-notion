<template>
  <!-- ナビゲーションバーをダークテーマで作成 -->
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <!-- タイトル -->
    <a class="navbar-brand" href="#">TechpitNotion</a>

    <!-- 画面サイズに応じて折りたたむ設定  -->
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarText" aria-controls="navbarText" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <!-- メニュー全体 -->
    <div class="collapse navbar-collapse" id="navbarText">
      <ul class="navbar-nav">
        <!-- ノートリストページへのリンク -->
        <li class="nav-item">
          <a class="nav-link" href="#"><i class="fas fa-file-alt"></i> ノートリスト</a>
        </li>

        <!-- 学習ページへのリンク -->
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" data-toggle="dropdown">
            <i class="fas fa-user-graduate"></i> 学習用ページ
          </a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">学習1</a></li>
            <li><a class="dropdown-item" href="#">学習2</a></li>
            <li><a class="dropdown-item" href="#">学習3</a></li>
          </ul>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
}
</script>

<style scoped>
.navigation-bar {
  height: 60px;
}
</style>
