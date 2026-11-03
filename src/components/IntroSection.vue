<template>
  <section class="intro" aria-label="Introduction">
    <div class="intro-inner">
      <div class="rule"></div>
      <div class="split">
        <p class="statement">
          <span class="years">12+</span><span class="rest"> years of experience working at the intersection of design &amp; development.</span>
        </p>
        <div class="support">
          <p>Specialized in translating product and design concepts into production-ready interfaces.</p>
          <p>Experienced in building design/development tools with AI integrations, design systems, ecommerce experiences, and component-driven products.</p>
        </div>
      </div>
      <div class="rule"></div>
    </div>
  </section>
</template>

<style scoped>
.intro {
  background: #F5F2EA;
  width: calc(100% + 60px);
  margin-left: -30px;
  margin-right: -30px;
  padding: 40px 24px 56px;
}

.intro-inner {
  display: flex;
  flex-direction: column;
  gap: 28px;
  max-width: 1200px;
  margin: 0 auto;
}

.rule {
  height: 1px;
  background: rgba(35, 62, 56, 0.18);
}

.split {
  display: flex;
  flex-direction: column;
  gap: 28px;
}

.statement {
  margin: 0;
  font-family: "Cormorant Garamond", Georgia, serif;
  font-weight: 400;
  color: #233e38;
  letter-spacing: -0.6px;
  line-height: 1.08;
}

.years {
  font-size: 64px;
}

.rest {
  font-size: 34px;
}

.support {
  display: flex;
  flex-direction: column;
  gap: 20px;
  font-family: "Cormorant Garamond", Georgia, serif;
  font-weight: 400;
  font-size: 20px;
  line-height: 1.4;
  color: #233e38;
}

.support p {
  margin: 0;
}

@media (min-width: 768px) {
  .intro {
    padding: 56px max(48px, min(120px, 8.333vw)) 88px;
  }

  .intro-inner {
    gap: 44px;
  }

  .split {
    flex-direction: row;
    align-items: center;
    gap: clamp(40px, 6.5vw, 96px);
  }

  .statement {
    flex: 1.3 1 0;
    min-width: 0;
    letter-spacing: -1.2px;
  }

  .years {
    font-size: clamp(72px, 6.6vw, 96px);
  }

  .rest {
    font-size: clamp(40px, 4vw, 58px);
  }

  .support {
    flex: 1 1 0;
    align-self: center;
    min-width: 0;
    gap: 28px;
    font-size: 24px;
    line-height: 1.35;
  }
}
</style>
