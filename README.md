# 3DRunning Worker

这是 3DRunning 项目的 Worker 依赖，用于解析 3D 模型文件（GLTF/GLB）并生成业务层级。  

This is a Worker dependency of the 3DRunning project and is used to parse the 3D model file (GLTF/GLB) and generate business hierarchies.

Worker 已打包为独立 ESM 文件，可直接从 CDN 加载，无需安装依赖。

Workers are packaged as separate ESM files that can be loaded directly from the CDN without installation dependencies.

---

## 🚀 使用方法

### 1. 创建 Worker(Create Worker)

```ts
const WORKER_URL = 'https://cdn.jsdelivr.net/gh/<username>/3drunning-worker@1.0.0/model.worker.js';

const worker = new Worker(WORKER_URL, { type: 'module' });
```

### 2. 发送消息给 Worker(Post Message)

```ts
worker.postMessage({
  type: 'PARSE',
  url: 'https://example.com/model.glb'
});
```

### 3. 接收 Worker 消息(Receive Message)

```ts
worker.onmessage = (event) => {
  const { type, payload, message } = event.data;

  switch (type) {
    case 'PARSE_COMPLETE':
      console.log('解析完成:', payload);
      break;
    case 'PARSE_ERROR':
      console.error('解析失败:', message);
      break;
  }
};
```