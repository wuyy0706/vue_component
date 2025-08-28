<template>
  <div class="virtual-scroller-demo">
    <div class="comparison">
      <div class="panel">
        <div class="panel-header">
          <h2>常规列表</h2>
          <span class="badge badge-danger">性能低</span>
        </div>
        <div class="list-container">
          <ul class="normal-list">
            <li v-for="item in normalList" :key="item.id" class="list-item">
              <span class="item-index">#{{ item.id }}</span>
              <span class="item-content">{{ item.content }}</span>
            </li>
          </ul>
        </div>
        <div class="stats">
          <p>渲染了 {{ normalList.length }} 个项目</p>
        </div>
      </div>

      <div class="panel">
        <div class="panel-header">
          <h2>Virtual Scroller</h2>
          <span class="badge badge-success">高性能</span>
        </div>
        <div class="list-container">
          <RecycleScroller
            class="scroller"
            :items="virtualList"
            :item-size="62"
            key-field="id"
          >
            <template v-slot="{ item }">
              <div class="list-item">
                <span class="item-index">#{{ item.id }}</span>
                <span class="item-content">{{ item.content }}</span>
              </div>
            </template>
          </RecycleScroller>
        </div>
        <div class="stats">
          <p>总共 {{ virtualList.length }} 个项目</p>
        </div>
      </div>
    </div>

    <div class="controls">
      <button @click="loadMore(1000)">加载1000条</button>
      <button @click="loadMore(5000)">加载5000条</button>
      <button @click="reset">重置列表</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VirtualScrollerDemo',
  data() {
    return {
      normalList: [],
      virtualList: [],
      itemCount: 1000
    }
  },
  created() {
    this.loadMore(this.itemCount)
  },
  methods: {
    loadMore(count) {
      const startId = this.normalList.length + 1
      for (let i = 0; i < count; i++) {
        const id = startId + i
        const item = {
          id: id,
          content: `项目 ${id} - ${this.randomText()}`
        }
        this.normalList.push(item)
        this.virtualList.push(item)
      }
      this.itemCount += count
    },
    reset() {
      this.normalList = []
      this.virtualList = []
      this.itemCount = 1000
      this.loadMore(this.itemCount)
    },
    randomText() {
      const texts = ["性能优化", "虚拟滚动", "Vue.js", "Web开发"]
      return texts[Math.floor(Math.random() * texts.length)]
    }
  }
}
</script>

<style scoped>
.virtual-scroller-demo {
  max-width: 1000px;
  margin: 0 auto;
  padding: 20px;
  background: white;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.comparison {
  display: flex;
  margin-bottom: 20px;
}

.panel {
  flex: 1;
  margin: 0 10px;
}

.panel-header {
  padding: 12px 15px;
  background: #2c3e50;
  color: white;
  display: flex;
  justify-content: space-between;
  border-radius: 6px 6px 0 0;
}

.badge {
  padding: 3px 8px;
  border-radius: 12px;
  font-size: 12px;
}

.badge-danger {
  background: #e74c3c;
}

.badge-success {
  background: #2ecc71;
}

.list-container {
  height: 400px;
  overflow: auto;
  border: 1px solid #e0e0e0;
  border-radius: 0 0 6px 6px;
}

.normal-list {
  padding: 0;
  margin: 0;
  list-style: none;
}

.list-item {
  padding: 12px 15px;
  border-bottom: 1px solid #eee;
  display: flex;
}

.item-index {
  font-weight: bold;
  margin-right: 10px;
  color: #7e8c9a;
  min-width: 30px;
}

.stats {
  padding: 12px 15px;
  background: #f8f9fa;
  border-top: 1px solid #e0e0e0;
  font-size: 13px;
  color: #666;
  border-radius: 0 0 6px 6px;
}

.scroller {
  height: 100%;
}

.controls {
  text-align: center;
}

button {
  padding: 8px 15px;
  background: #6a11cb;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin: 0 5px;
}

button:hover {
  background: #2575fc;
}
</style>