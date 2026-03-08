# 📄 功能玩法指南

想知道我们有哪些功能玩法？本页面将引导您快速了解学习我们制作的独特内容！

<div class="feature-cards">
  <a href="/features/base/economy" class="feature-card chat-card">
    <div class="feature-card-content">
      <h3>✨ 基础内容</h3>
      <p>我们的货币体系，领地如何创建，独特的小功能。</p>
    </div>
  </a>
</div>

<div class="feature-cards">
  <a href="/features/pastoral/builder" class="feature-card chat-card">
    <div class="feature-card-content">
      <h3>🌼 田园生活</h3>
      <p>只想搞搞建筑？走养老生存的路线。看看我们的季节、种植和食物等内容吧！</p>
    </div>
  </a>
</div>

<div class="feature-cards">
  <a href="/features/adventure/mmo/info" class="feature-card chat-card">
    <div class="feature-card-content">
      <h3>⚔️ 冒险与战斗</h3>
      <p>打怪升级，挑战自己。了解如何制作独特的装备，提升属性！</p>
    </div>
  </a>
</div>

有关常见问题的详细解答，请参考[常见问题](/manual/faq)页面

<style>
.feature-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  margin: 30px 0;
}

.feature-card {
  border-radius: 15px;
  padding: 25px;
  color: white !important;
  text-decoration: none !important;
  transition: all 0.3s ease;
  box-shadow: 0 8px 25px rgba(0,0,0,0.15);
  position: relative;
  overflow: hidden;
  cursor: pointer;
}

.feature-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 35px rgba(0,0,0,0.2);
}

.feature-card-content {
  position: relative;
  z-index: 2;
}

.feature-card h3 {
  margin: 0 0 15px 0;
  font-size: 1.4em;
  font-weight: 600;
  color: white;
}

.feature-card p {
  margin: 0;
  opacity: 0.9;
  line-height: 1.5;
  color: white;
}

.feature-card a {
  text-decoration: none !important;
  color: inherit !important;
}

/* 不同功能的颜色 */
.chat-card {
  background: linear-gradient(135deg, #3b82f6 0%, #1d4ed8 100%);
}

.personality-card {
  background: linear-gradient(135deg, #8b5cf6 0%, #7c3aed 100%);
}

.expression-card {
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
}

.memory-card {
  background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
}

.jargon-card {
  background: linear-gradient(135deg, #14b8a6 0%, #0d9488 100%);
}

.lpmm-card {
  background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%);
}

.emoji-card {
  background: linear-gradient(135deg, #ec4899 0%, #db2777 100%);
}
</style>
