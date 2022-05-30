![MasterHead](https://1.bp.blogspot.com/-7A4WynwLsMw/XbBpCXG8fHI/AAAAAAAAMt4/uOa1bpLskYgrwGbllhSu2SDj_Mig8SXJQCLcBGAsYHQ/s1600/2000_600px.gif)]
<h1 align="center">Hi 👋, I'm ahmet hassan</h1>
<h3 align="center">A passionate frontend developer from somalia</h3>#
<img align="right" alt="Coding" width="400" src="https://cdn.dribbble.com/users/926537/screenshots/4502924/python-2.gif">

@@ -46,7 +46,6 @@ const createTextNode = ({
  `;
};


/**
 * @param {Partial<import('../fetchers/types').StatsData>} stats
 * @param {Partial<import("./types").StatCardOptions>} options
@@ -239,9 +238,26 @@ const renderStatsCard = (stats = {}, options = { hide: [] }) => {

  if (disable_animations) card.disableAnimations();

  // Accessibility Labels
  const labels = Object.keys(STATS)
    .filter((key) => !hide.includes(key))
    .map((key) => {
      if (key === "commits") {
        return `${i18n.t("statcard.commits")} ${
          include_all_commits ? "" : `in ${new Date().getFullYear()}`
        } : ${totalStars}`;
      }
      return `${STATS[key].label}: ${STATS[key].value}`;
    })
    .join(", ");

  card.setAccessibilityLabel({
    title: `${card.title}, Rank: ${rank.level}`,
    desc: labels,
  });

  return card.render(`
    ${rankCircle}
    <svg x="0" y="0">
      ${flexLayout({
        items: statItems,
  14  
src/common/Card.js
@@ -42,12 +42,22 @@ class Card {
    this.paddingY = 35;
    this.titlePrefixIcon = titlePrefixIcon;
    this.animations = true;
    this.a11yTitle = "";
    this.a11yDesc = "";
  }

  disableAnimations() {
    this.animations = false;
  }

  /**
   * @param {{title: string, desc: string}} prop
   */
  setAccessibilityLabel({ title, desc }) {
    this.a11yTitle = title;
    this.a11yDesc = desc;
  }

  /**
   * @param {string} value
   */
@@ -148,7 +158,11 @@ class Card {
        viewBox="0 0 ${this.width} ${this.height}"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
        role="img"
        aria-labelledby="descId"
      >
        <title id="titleId">${this.a11yTitle}</title>
        <desc id="descId">${this.a11yDesc}</desc>
        <style>
          .header {
            font: 600 18px 'Segoe UI', Ubuntu, Sans-Serif;
  8  
tests/__snapshots__/renderWakatimeCard.test.js.snap
@@ -8,7 +8,11 @@ exports[`Test Render Wakatime Card should render correctly 1`] = `
        viewBox=\\"0 0 495 150\\"
        fill=\\"none\\"
        xmlns=\\"http://www.w3.org/2000/svg\\"
        role=\\"img\\"
        aria-labelledby=\\"descId\\"
      >
        <title id=\\"titleId\\"></title>
        <desc id=\\"descId\\"></desc>
        <style>
          .header {
            font: 600 18px 'Segoe UI', Ubuntu, Sans-Serif;
@@ -165,7 +169,11 @@ exports[`Test Render Wakatime Card should render correctly with compact layout 1
        viewBox=\\"0 0 495 115\\"
        fill=\\"none\\"
        xmlns=\\"http://www.w3.org/2000/svg\\"
        role=\\"img\\"
        aria-labelledby=\\"descId\\"
      >
        <title id=\\"titleId\\"></title>
        <desc id=\\"descId\\"></desc>
        <style>
          .header {
            font: 600 18px 'Segoe UI', Ubuntu, Sans-Serif;
