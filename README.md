<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Task Force CAN 2027 – France Sport Expertise</title>
<link href="https://fonts.googleapis.com/css2?family=Geologica:wght@300;400;700&display=swap" rel="stylesheet">
<style>
  :root {
    --navy:   #2D2D7F;
    --blue2:  #4A6FA5;
    --blue3:  #6B9FD4;
    --gold:   #F0B429;
    --white:  #FFFFFF;
    --off:    #F7F8FC;
    --border: #E2E6F0;
    --text:   #1A1A3A;
    --muted:  #6B7280;
    --p-bg:   #EAF4EE;
    --p-fg:   #1A6B3A;
    --o-bg:   #FEF3DC;
    --o-fg:   #7A4F00;
    --s-bg:   #F0F0F8;
    --s-fg:   #4A4A8A;
    --radius: 8px;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'Geologica', sans-serif; background: var(--off); color: var(--text); font-size: 13px; }

  /* HEADER */
  header {
    background: var(--navy);
    padding: 18px 32px;
    display: flex; align-items: center; gap: 20px;
    border-bottom: 3px solid var(--gold);
  }
  header img { height: 48px; filter: brightness(0) invert(1); }
  .header-text h1 { color: var(--white); font-size: 17px; font-weight: 700; letter-spacing: .04em; }
  .header-text p { color: rgba(255,255,255,.65); font-size: 11px; font-weight: 300; margin-top: 2px; }

  /* FILTERS */
  .filters {
    background: var(--white);
    padding: 12px 32px;
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 24px; flex-wrap: wrap;
  }
  .filters label { font-size: 11px; font-weight: 700; color: var(--navy); text-transform: uppercase; letter-spacing: .06em; }
  .filter-group { display: flex; gap: 6px; flex-wrap: wrap; }
  .fbtn {
    padding: 4px 12px; border-radius: 20px; border: 1.5px solid var(--border);
    background: var(--white); color: var(--muted); font-family: 'Geologica', sans-serif;
    font-size: 11px; cursor: pointer; transition: all .15s;
  }
  .fbtn:hover { border-color: var(--navy); color: var(--navy); }
  .fbtn.active { background: var(--navy); color: var(--white); border-color: var(--navy); }
  .fbtn.gold.active { background: var(--gold); color: var(--navy); border-color: var(--gold); }

  /* TABS */
  .tabs {
    display: flex; gap: 0;
    background: var(--white);
    border-bottom: 2px solid var(--border);
    padding: 0 32px;
  }
  .tab {
    padding: 12px 20px; cursor: pointer; font-size: 12px; font-weight: 700;
    color: var(--muted); border-bottom: 3px solid transparent; margin-bottom: -2px;
    text-transform: uppercase; letter-spacing: .05em; transition: all .15s;
  }
  .tab:hover { color: var(--navy); }
  .tab.active { color: var(--navy); border-bottom-color: var(--gold); }

  /* MAIN */
  main { padding: 24px 32px; max-width: 1400px; margin: 0 auto; }
  .view { display: none; }
  .view.active { display: block; }

  /* PRIORITY BADGES */
  .badge {
    display: inline-block; padding: 2px 8px; border-radius: 20px;
    font-size: 10px; font-weight: 700; text-transform: uppercase; letter-spacing: .05em; white-space: nowrap;
  }
  .badge-haute   { background: var(--p-bg); color: var(--p-fg); }
  .badge-opportunite { background: var(--o-bg); color: var(--o-fg); }
  .badge-surveiller  { background: var(--s-bg); color: var(--s-fg); }

  .pays-tag {
    display: inline-block; padding: 2px 8px; border-radius: 4px;
    font-size: 10px; font-weight: 400; background: #EEF2FF; color: var(--navy);
  }

  /* ── VIEW 1 : PRESCRIPTEURS ── */
  .opp-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(360px,1fr)); gap: 16px; }
  .opp-card {
    background: var(--white); border: 1px solid var(--border); border-radius: var(--radius);
    padding: 18px; display: flex; flex-direction: column; gap: 10px;
    transition: box-shadow .15s;
  }
  .opp-card:hover { box-shadow: 0 4px 16px rgba(45,45,127,.10); }
  .opp-card.hidden { display: none; }
  .opp-header { display: flex; justify-content: space-between; align-items: flex-start; gap: 8px; }
  .opp-presc { font-weight: 700; font-size: 13px; color: var(--navy); line-height: 1.3; }
  .opp-contact { font-size: 11px; color: var(--muted); margin-top: 2px; }
  .opp-domaine { font-size: 12px; font-weight: 700; color: var(--text); border-left: 3px solid var(--gold); padding-left: 8px; }
  .opp-desc { font-size: 11px; color: var(--muted); line-height: 1.5; }
  .opp-meta { display: flex; gap: 6px; align-items: center; flex-wrap: wrap; }
  .echeance { font-size: 10px; color: var(--muted); }

  .members-section { display: flex; flex-direction: column; gap: 6px; }
  .members-label { font-size: 10px; font-weight: 700; text-transform: uppercase; letter-spacing: .06em; color: var(--muted); }
  .member-chips { display: flex; flex-wrap: wrap; gap: 4px; }
  .chip {
    padding: 3px 9px; border-radius: 4px; font-size: 11px;
    border: 1px solid transparent; cursor: default;
  }
  .chip-tf  { background: #EEF2FF; color: var(--navy); border-color: #C7D2FE; }
  .chip-sol { background: #FFFBEB; color: #92400E; border-color: #FDE68A; }

  /* TOOLTIP */
  .chip-tf-wrap { position: relative; display: inline-block; margin-bottom: 4px; }
  .chip-tf-wrap .tooltip {
    display: none;
    position: absolute;
    left: 0; top: calc(100% + 6px);
    background: var(--navy);
    color: var(--white);
    font-size: 11px; line-height: 1.7;
    padding: 10px 14px;
    border-radius: 6px;
    min-width: 280px; max-width: 360px;
    z-index: 100;
    box-shadow: 0 4px 16px rgba(0,0,0,.18);
    pointer-events: none;
  }
  .chip-tf-wrap .tooltip ul { list-style: none; padding: 0; margin: 0; }
  .chip-tf-wrap .tooltip li { padding-left: 12px; position: relative; }
  .chip-tf-wrap .tooltip li::before { content: "·"; position: absolute; left: 0; color: var(--gold); font-weight: 700; }
  .chip-tf-wrap:hover .tooltip { display: block; }
  .chip-tf-wrap .chip-tf { cursor: default; }
  .chip-tf-wrap .has-refs .chip-tf { border-bottom: 1.5px dashed var(--blue2); cursor: help; }
  /* refs-list used in member view */
  .refs-list {
    background: var(--off); border-radius: 4px; padding: 8px 10px;
    font-size: 11px; color: var(--muted); line-height: 1.8;
  }
  .refs-list li { list-style: none; padding-left: 10px; position: relative; }
  .refs-list li::before { content: "·"; position: absolute; left: 0; color: var(--gold); font-weight: 700; }

  /* ── VIEW 2 : MEMBRES ── */
  .member-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(320px,1fr)); gap: 16px; }
  .member-card {
    background: var(--white); border: 1px solid var(--border); border-radius: var(--radius);
    padding: 18px; display: flex; flex-direction: column; gap: 10px;
    transition: box-shadow .15s;
  }
  .member-card:hover { box-shadow: 0 4px 16px rgba(45,45,127,.10); }
  .member-card.hidden { display: none; }
  .member-name { font-size: 15px; font-weight: 700; color: var(--navy); }
  .member-sector { font-size: 11px; color: var(--muted); font-weight: 300; }
  .member-xaw { font-size: 10px; color: var(--muted); font-style: italic; background: var(--off); padding: 4px 8px; border-radius: 4px; }
  .stat-row { display: flex; gap: 12px; }
  .stat-box { text-align: center; flex: 1; background: var(--off); border-radius: 6px; padding: 8px 4px; }
  .stat-n { font-size: 20px; font-weight: 700; color: var(--navy); }
  .stat-l { font-size: 9px; color: var(--muted); text-transform: uppercase; letter-spacing: .04em; }
  .member-opps { display: flex; flex-direction: column; gap: 4px; }
  .member-opp-item {
    font-size: 11px; padding: 4px 8px; border-radius: 4px;
    border-left: 3px solid transparent; background: var(--off);
    display: flex; justify-content: space-between; align-items: center; gap: 8px;
  }
  .member-opp-item.haute     { border-left-color: var(--p-fg); }
  .member-opp-item.opportunite { border-left-color: var(--o-fg); }
  .member-opp-item.surveiller  { border-left-color: var(--s-fg); }
  .member-opp-label { flex: 1; line-height: 1.3; }

  /* ── VIEW 3 : MATRICE ── */
  .matrix-section { margin-bottom: 40px; }
  .matrix-title { font-size: 14px; font-weight: 700; color: var(--navy); margin-bottom: 4px; }
  .matrix-subtitle { font-size: 11px; color: var(--muted); margin-bottom: 14px; }
  .matrix-legend { display: flex; gap: 16px; margin-bottom: 14px; flex-wrap: wrap; }
  .leg-item { display: flex; align-items: center; gap: 6px; font-size: 11px; }
  .leg-dot { width: 12px; height: 12px; border-radius: 3px; }

  .matrix-wrap { overflow-x: auto; }
  table.matrix {
    border-collapse: collapse; width: max-content; min-width: 100%;
  }
  table.matrix th, table.matrix td {
    padding: 0; border: 1px solid var(--border);
  }
  table.matrix .col-member {
    padding: 8px 12px; font-size: 11px; font-weight: 700; color: var(--navy);
    background: var(--white); white-space: nowrap; min-width: 160px;
    position: sticky; left: 0; z-index: 2; border-right: 2px solid var(--border);
  }
  table.matrix .col-header {
    writing-mode: vertical-lr; transform: rotate(180deg);
    padding: 10px 6px; font-size: 10px; font-weight: 700; color: var(--navy);
    background: var(--off); min-width: 36px; max-width: 36px; text-align: left;
    white-space: nowrap;
  }
  table.matrix .corner {
    background: var(--off); position: sticky; left: 0; z-index: 3;
    min-width: 160px;
  }
  table.matrix .cell {
    text-align: center; vertical-align: middle; min-width: 36px; height: 32px;
    font-size: 11px; font-weight: 700;
  }
  table.matrix .cell-haute       { background: var(--p-bg); color: var(--p-fg); }
  table.matrix .cell-opportunite { background: var(--o-bg); color: var(--o-fg); }
  table.matrix .cell-surveiller  { background: var(--s-bg); color: var(--s-fg); }
  table.matrix .cell-empty       { background: var(--white); color: #CCC; }
  table.matrix .cell-count {
    background: var(--navy); color: var(--white);
    font-size: 11px; font-weight: 700; text-align: center; vertical-align: middle;
    height: 32px;
  }
  table.matrix .row-count td {
    background: #F0F2FA; font-size: 10px; font-weight: 700;
    text-align: center; color: var(--navy); height: 28px; vertical-align: middle;
  }
  table.matrix .row-count .col-member {
    background: #F0F2FA; font-size: 10px; color: var(--navy); text-align: left;
  }
  table.matrix .sector-label {
    font-size: 9px; font-weight: 300; color: var(--muted); display: block;
  }

  /* EMPTY STATE */
  .empty-state { text-align: center; padding: 60px 20px; color: var(--muted); font-size: 13px; }

  /* RESPONSIVE */
  @media (max-width: 768px) {
    header { padding: 14px 16px; }
    main { padding: 16px; }
    .filters { padding: 10px 16px; }
    .tabs { padding: 0 16px; }
  }
</style>
</head>
<body>

<header>
  <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABC8AAAJBCAYAAABmn58tAAAACXBIWXMAACE3AAAhNwEzWJ96AAAgAElEQVR4nOzBMQEAAADCoPVPbQ0PIAAAAIBb1QAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg+lc9GzsgQQAAAOBXNQAAAP//7MMxDQAAAMOg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4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA///swzENAAAAw6D6Vz0bOyBBAAAA4Fc1AAAA//8DACYQVyFrbryeAAAAAElFTkSuQmCC" alt="France Sport Expertise">
  <div class="header-text">
    <h1>Task Force CAN 2027 — Positionnement membres</h1>
    <p>Kenya · Tanzanie · Ouganda · Égypte &nbsp;|&nbsp; Mission Nairobi, Mai 2026 &nbsp;|&nbsp; Usage interne &amp; externe FSE</p>
  </div>
</header>

<div class="filters">
  <label>Pays</label>
  <div class="filter-group" id="filter-pays">
    <button class="fbtn active" data-pays="tous">Tous</button>
    <button class="fbtn" data-pays="Kenya">Kenya</button>
    <button class="fbtn" data-pays="Tanzanie">Kenya · Tanzanie</button>
    <button class="fbtn" data-pays="Ouganda">Multi-pays</button>
    <button class="fbtn" data-pays="Égypte">Égypte</button>
  </div>
  <label style="margin-left:16px">Priorité</label>
  <div class="filter-group" id="filter-prio">
    <button class="fbtn active" data-prio="tous">Toutes</button>
    <button class="fbtn" data-prio="haute">Priorité haute</button>
    <button class="fbtn" data-prio="opportunite">Opportunité</button>
    <button class="fbtn" data-prio="surveiller">À surveiller</button>
  </div>
</div>

<div class="tabs">
  <div class="tab active" data-view="prescripteurs">Par prescripteur</div>
  <div class="tab" data-view="membres">Par membre</div>
  <div class="tab" data-view="matrice">Couverture sectorielle</div>
</div>

<main>
  <!-- VIEW 1 -->
  <div class="view active" id="view-prescripteurs">
    <div class="opp-grid" id="opp-grid"></div>
  </div>

  <!-- VIEW 2 -->
  <div class="view" id="view-membres">
    <div class="member-grid" id="member-grid"></div>
  </div>

  <!-- VIEW 3 -->
  <div class="view" id="view-matrice">
    <div class="matrix-legend">
      <div class="leg-item"><div class="leg-dot" style="background:var(--p-bg);border:1.5px solid var(--p-fg)"></div><span style="color:var(--p-fg);font-weight:700">P — Priorité haute</span></div>
      <div class="leg-item"><div class="leg-dot" style="background:var(--o-bg);border:1.5px solid var(--o-fg)"></div><span style="color:var(--o-fg);font-weight:700">O — Opportunité</span></div>
      <div class="leg-item"><div class="leg-dot" style="background:var(--s-bg);border:1.5px solid var(--s-fg)"></div><span style="color:var(--s-fg);font-weight:700">S — À surveiller</span></div>
      <div class="leg-item"><div class="leg-dot" style="background:var(--white);border:1px solid var(--border)"></div><span style="color:var(--muted)">— Non positionné</span></div>
    </div>

    <div class="matrix-section">
      <div class="matrix-title">Matrice membres × domaines d'opportunité</div>
      <div class="matrix-subtitle">Chaque colonne représente un domaine d'opportunité identifié lors de la mission Nairobi</div>
      <div class="matrix-wrap" id="matrix-domains"></div>
    </div>

    <div class="matrix-section">
      <div class="matrix-title">Matrice membres × prescripteurs</div>
      <div class="matrix-subtitle">Chaque colonne représente un prescripteur / interlocuteur rencontré</div>
      <div class="matrix-wrap" id="matrix-prescripteurs"></div>
    </div>
  </div>
</main>

<script>
const OPPS = [{"id": 0, "prescripteur": "LOC CAN 2027 Kenya", "contact": "Tony Lungaho, CEO", "pays": "Kenya", "echeance": "2026\u20132027", "domaine": "Marketing & Activation commerciale", "description": "Marketing, broadcast rights et activation commerciale autour de l'AFCON 2027", "priorite": "haute", "membres_tf": ["Keneo", "Eventeam", "Spartner"], "membres_sol": ["Auditoire", "Playground"]}, {"id": 1, "prescripteur": "LOC CAN 2027 Kenya", "contact": "", "pays": "Kenya", "echeance": "2026\u20132027", "domaine": "Fan zones & dispositifs terrain", "description": "Cr\u00e9ation de fan zones et dispositifs de fan engagement dans tout le Kenya", "priorite": "haute", "membres_tf": ["Keneo", "Eventeam", "Orange Events", "Spartner", "Natural Grass", "Armonia/THA"], "membres_sol": ["Auditoire", "Playground"]}, {"id": 2, "prescripteur": "LOC CAN 2027 \u2013 Coop\u00e9ration r\u00e9gionale", "contact": "Contact CEO Tanzanie \u00e9tabli", "pays": "Kenya \u00b7 Tanzanie \u00b7 Ouganda", "echeance": "2026\u20132027", "domaine": "Coop\u00e9ration r\u00e9gionale", "description": "Structuration d'une coop\u00e9ration r\u00e9gionale entre les 3 pays h\u00f4tes", "priorite": "haute", "membres_tf": ["Keneo", "Eventeam", "Spartner", "GL Events"], "membres_sol": []}, {"id": 3, "prescripteur": "LOC CAN 2027 Kenya + Tanzanie", "contact": "", "pays": "Kenya \u00b7 Tanzanie", "echeance": "2026\u20132027", "domaine": "Tourisme sportif & hospitalit\u00e9", "description": "D\u00e9veloppement du tourisme sportif et des offres VIP / hospitalit\u00e9", "priorite": "haute", "membres_tf": ["Orange Events", "Eventeam", "Keneo", "Spartner", "Armonia/THA"], "membres_sol": ["Petit Forestier", "MyComm"]}, {"id": 4, "prescripteur": "Minist\u00e8re des Sports du Kenya", "contact": "Hon. Elijah Mwangri, Principal Secretary", "pays": "Kenya", "echeance": "2026\u20132030", "domaine": "Cr\u00e9ation & modernisation de stades", "description": "Modernisation ou d\u00e9veloppement de stades \u2013 cr\u00e9ation de 30 nouveaux stades (ing\u00e9nierie, \u00e9quipements, technologies VAR)", "priorite": "haute", "membres_tf": ["Osmose Ing\u00e9nierie", "Alcor \u00c9quipements", "Metalu-Plast", "Cryo Control", "GL Events", "Loxam", "VOGO"], "membres_sol": ["DIMASPORT"]}, {"id": 5, "prescripteur": "Minist\u00e8re des Sports du Kenya", "contact": "", "pays": "Kenya", "echeance": "2026\u20132030", "domaine": "Exploitation & activation de stades", "description": "Accompagnement de l'exploitation durable du Talanta Stadium \u2013 activation \u00e9v\u00e9nementielle annuelle", "priorite": "haute", "membres_tf": ["Orange Events", "Keneo", "Eventeam", "GL Events", "Loxam", "Spartner", "Armonia/THA"], "membres_sol": []}, {"id": 6, "prescripteur": "Minist\u00e8re des Sports du Kenya", "contact": "", "pays": "Kenya", "echeance": "2026\u20132030", "domaine": "D\u00e9veloppement de la pratique sportive", "description": "D\u00e9veloppement de la pratique sportive au Kenya \u2013 fort besoin en mat\u00e9riels", "priorite": "opportunite", "membres_tf": ["Osmose Ing\u00e9nierie", "Metalu-Plast", "Cryo Control"], "membres_sol": ["DIMASPORT"]}, {"id": 7, "prescripteur": "Talanta Stadium / CRBC", "contact": "Constructeur chinois \u2013 livraison juillet 2026", "pays": "Kenya", "echeance": "2026", "domaine": "Exploitation post-livraison", "description": "Stade 60 000 places livr\u00e9 en juillet 2026 \u2013 opportunit\u00e9 sur l'exploitation et les services", "priorite": "opportunite", "membres_tf": ["Orange Events", "GL Events", "Natural Grass", "Spartner", "Armonia/THA"], "membres_sol": ["MyComm"]}, {"id": 8, "prescripteur": "CNO Kenya", "contact": "Francis N. Karugu", "pays": "Kenya", "echeance": "2026\u20132030", "domaine": "Infrastructures sportives r\u00e9gionales", "description": "Accompagnement dans le d\u00e9veloppement des infrastructures sportives r\u00e9gionales (incl. piste d'athl\u00e9tisme)", "priorite": "opportunite", "membres_tf": ["Osmose Ing\u00e9nierie", "Metalu-Plast", "Cryo Control", "Keneo", "Eventeam", "Spartner", "Natural Grass", "Alcor \u00c9quipements"], "membres_sol": ["DIMASPORT"]}, {"id": 9, "prescripteur": "CNO Kenya", "contact": "", "pays": "Kenya", "echeance": "2026\u20132030", "domaine": "Politiques publiques & haute performance", "description": "Accompagnement dans les politiques publiques de d\u00e9veloppement de la pratique et de la haute performance", "priorite": "surveiller", "membres_tf": ["Keneo", "Eventeam", "Spartner"], "membres_sol": ["MyCoach"]}, {"id": 10, "prescripteur": "Kenya Sports Academy", "contact": "Projet gouvernemental", "pays": "Kenya", "echeance": "2027\u20132030", "domaine": "Campus sportif national", "description": "Acad\u00e9mie sportive de 200 ha \u2013 30 terrains sportifs + campus national \u2013 partenariat gouvernement fran\u00e7ais souhait\u00e9", "priorite": "opportunite", "membres_tf": ["Osmose Ing\u00e9nierie", "Metalu-Plast", "Cryo Control", "Keneo", "Eventeam", "Spartner", "Natural Grass"], "membres_sol": ["DIMASPORT"]}, {"id": 11, "prescripteur": "Aegis Sport Academy", "contact": "", "pays": "Kenya", "echeance": "2026\u20132027", "domaine": "\u00c9quipements & infrastructures acad\u00e9mie", "description": "Acad\u00e9mie priv\u00e9e \u2013 importants besoins en infrastructures et \u00e9quipements sportifs", "priorite": "surveiller", "membres_tf": ["Osmose Ing\u00e9nierie", "Metalu-Plast", "Cryo Control", "Loxam"], "membres_sol": ["DIMASPORT"]}, {"id": 12, "prescripteur": "CNO \u00c9gypte", "contact": "Yasser Ibrahim Idris, Pr\u00e9sident", "pays": "\u00c9gypte", "echeance": "2027", "domaine": "Jeux africains 2027", "description": "L'\u00c9gypte organise les Jeux africains 2027 \u2013 accompagnement op\u00e9rationnel recherch\u00e9", "priorite": "haute", "membres_tf": ["Cryo Control", "Orange Events", "Keneo", "Eventeam", "GL Events", "Armonia/THA", "VOGO"], "membres_sol": []}, {"id": 13, "prescripteur": "CNO \u00c9gypte", "contact": "", "pays": "\u00c9gypte", "echeance": "2036\u20132040", "domaine": "Candidature olympique \u2013 conseil strat\u00e9gique", "description": "Conseil strat\u00e9gique pour une candidature aux JO 2036/2040", "priorite": "opportunite", "membres_tf": ["Eventeam", "Keneo", "Spartner"], "membres_sol": []}, {"id": 14, "prescripteur": "CNO \u00c9gypte", "contact": "", "pays": "\u00c9gypte", "echeance": "2027\u20132030", "domaine": "D\u00e9veloppement infrastructures sportives", "description": "D\u00e9veloppement des infrastructures sportives en \u00c9gypte (incl. piste d'athl\u00e9tisme, gazon synth\u00e9tique)", "priorite": "opportunite", "membres_tf": ["Osmose Ing\u00e9nierie", "Metalu-Plast", "Cryo Control", "Natural Grass", "GL Events"], "membres_sol": ["DIMASPORT"]}];
const MEMBERS = [{"name": "Keneo", "sector": "Event Design & Exp\u00e9rience", "refs": ["CAN 2017 (x2)", "FIFA WC 2026 Maroc (conseil candidature)", "Filiale H\u00e9rije Dakar (S\u00e9n\u00e9gal)", "JOP Paris 2024 Fan zones \u00b7 UEFA CL 2022 Fan zone \u00b7 Inde 2036 candidature JO"], "opps": [0, 1, 2, 3, 5, 9, 10, 12, 13], "xaw": false}, {"name": "Eventeam", "sector": "Event Design & Exp\u00e9rience", "refs": ["CAN 2017 Gabon", "Candidature Maroc CDM 2026 (conseil)", "JOP 2012 / 2016 / 2024 hospitalit\u00e9s", "CDM Football 2018 / 2022 hospitalit\u00e9s \u00b7 Jeux Asiatiques 2026"], "opps": [0, 1, 2, 3, 5, 9, 10, 12, 13], "xaw": false}, {"name": "Spartner", "sector": "Planification op\u00e9rationnelle", "refs": ["Conseil FRMF \u2013 FIFA CDM 2030 Maroc", "Conseil Commission Royale Riyad \u2013 FIFA CDM 2034", "JOP Paris 2024 (4 stades football, 27 matchs)", "Programmes AFD (Maroc, Rwanda) \u00b7 RWC 2023"], "opps": [0, 1, 2, 3, 5, 7, 8, 9, 10, 13], "xaw": false}, {"name": "GL Events", "sector": "Planification op\u00e9rationnelle", "refs": ["FIFA CDM Qatar 2022 (IBC)", "Contrat AFC annuel 2025-2026", "JOP Paris 2024 (53 sites)", "UEFA CL finals 2022-2025", "FIFA CDM Br\u00e9sil 2014 & Afrique du Sud 2010"], "opps": [2, 4, 5, 7, 12, 14], "xaw": false}, {"name": "Orange Events", "sector": "Smart Event & Technologie", "refs": ["CAN 2024 & 2025 (Orange Maroc)", "GITEX Africa Maroc", "JOP Paris 2024 \u00b7 RWC 2023", "UEFA CL annuel \u00b7 Pr\u00e9sence locale Orange Maroc"], "opps": [1, 3, 5, 7, 12], "xaw": false}, {"name": "Armonia/THA", "sector": "Hospitalit\u00e9 & Exp\u00e9rience guests", "refs": ["CAN 2025 Maroc (b\u00e9n\u00e9voles + accueil VIP)", "CHAN 2018 Maroc", "CDM Clubs FIFA 2013-2014 Maroc", "EXPO 2025 Osaka \u00b7 COP28 EAU \u00b7 GITEX Africa Maroc"], "opps": [1, 3, 5, 7, 12], "xaw": false}, {"name": "Osmose Ing\u00e9nierie", "sector": "Infrastructure & \u00c9quipements sportifs", "refs": ["Stade de Toulouse UEFA Euro 2016 & RWC 2023", "INF Clairefontaine", "Stade de France \u2013 piste athl\u00e9tisme JOP Paris 2024", "Stade Bollaert Lens Euro 2016"], "opps": [4, 6, 8, 10, 11, 14], "xaw": false}, {"name": "Metalu-Plast", "sector": "Infrastructure & \u00c9quipements sportifs", "refs": ["CAN 2025 Maroc (8 stades)", "CAN 2023 C\u00f4te d'Ivoire", "FIFA CDM 2018 Russie", "Acad\u00e9mie Mahd 2023 Arabie Saoudite \u00b7 NEOM Sports Hall 2025"], "opps": [4, 6, 8, 10, 11, 14], "xaw": false}, {"name": "Cryo Control", "sector": "Infrastructure & \u00c9quipements sportifs", "refs": ["CAN 2025 Maroc (8 stades, 32 installations)", "JOP Paris 2024 (100 bains)", "Fournisseur officiel JO depuis Londres 2012", "INSEP \u00b7 Clairefontaine \u00b7 AS Monaco \u00b7 PSG"], "opps": [4, 6, 8, 10, 11, 12, 14], "xaw": false}, {"name": "Alcor \u00c9quipements", "sector": "Infrastructure & \u00c9quipements sportifs", "refs": ["CAN 2019 Cameroun (80 000 si\u00e8ges)", "CAN 2021 U20 Mauritanie", "CAN 2023 CDI Yamoussoukro", "UEFA Euro 2016 (Bordeaux + Lyon) \u00b7 JOP Paris 2024"], "opps": [4, 8], "xaw": false}, {"name": "Loxam", "sector": "Infrastructure modulaire & durable", "refs": ["Fournisseur officiel JOP Paris 2024", "IBC JOP Paris 2024 (40 000 m\u00b2)", "UEFA CL finals 2022-2025", "IBC RWC 2023", "CDM F\u00e9minine FIFA 2019"], "opps": [4, 5, 11], "xaw": false}, {"name": "Natural Grass", "sector": "Infrastructure & \u00c9quipements sportifs", "refs": ["FRMF Centre Ma\u00e2mora (6 terrains hybrides) 2024-2026", "FRMF Taghazout (4 terrains hybrides)", "Real Madrid Bernab\u00e9u \u00b7 PSG \u00b7 OM \u00b7 Arsenal"], "opps": [1, 7, 8, 10, 14], "xaw": false}, {"name": "VOGO", "sector": "Smart Event & Technologie", "refs": ["FIFA CDM Qatar 2022 \u2013 syst\u00e8mes VAR", "Certifi\u00e9 FIFA VAR / VAR Light / VOL depuis 2023", "JOP Paris 2024 \u00b7 UEFA audio arbitres", "Ligue 1 partenaire officiel VAR"], "opps": [4, 12], "xaw": false}, {"name": "XAW Sports", "sector": "Planification op\u00e9rationnelle", "refs": ["15 \u00e9ditions des Jeux Olympiques", "350 \u00e9v\u00e9nements sportifs majeurs", "Coupe d'Asie AFC 2011 Qatar \u00b7 JOP Paris 2024", "Expert s\u00e9curit\u00e9 & gestion des risques"], "opps": [], "xaw": true}];
const DOMAINS = ["Marketing & Activation", "Fan zones & terrain", "Coop\u00e9ration r\u00e9gionale", "Tourisme & hospitalit\u00e9", "Cr\u00e9ation stades", "Exploitation stades", "Pratique sportive", "Talanta \u2013 post-livraison", "Infra. r\u00e9gionales CNO Kenya", "Politiques publiques", "Kenya Sports Academy", "Aegis Academy", "Jeux africains 2027", "Candidature olympique", "Infra. sportives \u00c9gypte"];

const PRESC_SHORT = [
  "LOC – Marketing","LOC – Fan zones","LOC – Coopération","LOC – Tourisme",
  "Min. Sports – Stades","Min. Sports – Exploit.","Min. Sports – Pratique",
  "Talanta Stadium","CNO Kenya – Infra.","CNO Kenya – Politique",
  "Kenya Sports Acad.","Aegis Academy",
  "CNO Égypte – JA 2027","CNO Égypte – JO cand.","CNO Égypte – Infra."
];

let filterPays = "tous";
let filterPrio = "tous";

// ── BADGE ────────────────────────────────────────────────────────────────────
function badge(p) {
  const labels = { haute: "Priorité haute", opportunite: "Opportunité", surveiller: "À surveiller" };
  return `<span class="badge badge-${p}">${labels[p]}</span>`;
}

// ── VIEW 1 : PRESCRIPTEURS ───────────────────────────────────────────────────
function renderOpps() {
  const grid = document.getElementById("opp-grid");
  grid.innerHTML = "";
  let shown = 0;

  OPPS.forEach(o => {
    const matchPays = filterPays === "tous" ||
      (filterPays === "Kenya" && o.pays === "Kenya") ||
      (filterPays === "Tanzanie" && o.pays.includes("Tanzanie")) ||
      (filterPays === "Ouganda" && o.pays.includes("Ouganda")) ||
      (filterPays === "Égypte" && o.pays.includes("Égypte"));
    const matchPrio = filterPrio === "tous" || o.priorite === filterPrio;

    if (!matchPays || !matchPrio) return;
    shown++;

    // Collect refs for TF members
    const tfRefsHtml = o.membres_tf.map(m => {
      const mdata = MEMBERS.find(x => x.name === m);
      const refs = mdata ? mdata.refs : [];
      const refsHtml = refs.length ? `<ul class="refs-list" id="refs-${o.id}-${m.replace(/[^a-zA-Z]/g,'')}">` + refs.map(r => `<li>${r}</li>`).join("") + `</ul>` : "";
      const toggle = refs.length ? `<span class="refs-toggle" onclick="toggleRefs('refs-${o.id}-${m.replace(/[^a-zA-Z]/g,'')}',${o.id},${JSON.stringify(m)})">Voir références</span>` : "";
      return `<div style="margin-bottom:6px"><span class="chip chip-tf">${m}</span> ${toggle}${refsHtml}</div>`;
    }).join("");

    const solHtml = o.membres_sol.length
      ? `<div class="members-section">
           <div class="members-label">À solliciter</div>
           <div class="member-chips">${o.membres_sol.map(m => `<span class="chip chip-sol">${m}</span>`).join("")}</div>
         </div>` : "";

    const card = document.createElement("div");
    card.className = "opp-card";
    card.innerHTML = `
      <div class="opp-header">
        <div>
          <div class="opp-presc">${o.prescripteur}</div>
          ${o.contact ? `<div class="opp-contact">${o.contact}</div>` : ""}
        </div>
        ${badge(o.priorite)}
      </div>
      <div class="opp-meta">
        <span class="pays-tag">${o.pays}</span>
        <span class="echeance">${o.echeance}</span>
      </div>
      <div class="opp-domaine">${o.domaine}</div>
      <div class="opp-desc">${o.description}</div>
      <div class="members-section">
        <div class="members-label">Membres TF positionnés</div>
        ${tfRefsHtml}
      </div>
      ${solHtml}
    `;
    grid.appendChild(card);
  });

  if (shown === 0) {
    grid.innerHTML = `<div class="empty-state">Aucune opportunité ne correspond aux filtres sélectionnés.</div>`;
  }
}

// tooltips handled via CSS hover

// ── VIEW 2 : MEMBRES ─────────────────────────────────────────────────────────
function renderMembers() {
  const grid = document.getElementById("member-grid");
  grid.innerHTML = "";

  MEMBERS.forEach(m => {
    const opps = m.opps.map(i => OPPS[i]).filter(o => {
      const matchPays = filterPays === "tous" ||
        (filterPays === "Kenya" && o.pays === "Kenya") ||
        (filterPays === "Tanzanie" && o.pays.includes("Tanzanie")) ||
        (filterPays === "Ouganda" && o.pays.includes("Ouganda")) ||
        (filterPays === "Égypte" && o.pays.includes("Égypte"));
      const matchPrio = filterPrio === "tous" || o.priorite === filterPrio;
      return matchPays && matchPrio;
    });

    const card = document.createElement("div");
    card.className = "member-card";

    const nHaute = opps.filter(o => o.priorite === "haute").length;
    const nOpp   = opps.filter(o => o.priorite === "opportunite").length;
    const nWatch = opps.filter(o => o.priorite === "surveiller").length;

    const oppItems = opps.map(o =>
      `<div class="member-opp-item ${o.priorite}">
        <div class="member-opp-label">${o.prescripteur} — ${o.domaine}</div>
        ${badge(o.priorite)}
       </div>`
    ).join("");

    const refsHtml = m.refs.length
      ? `<div class="members-section">
           <div class="members-label">Références clés</div>
           <ul class="refs-list" style="display:block">${m.refs.map(r=>`<li>${r}</li>`).join("")}</ul>
         </div>` : "";

    card.innerHTML = `
      <div>
        <div class="member-name">${m.name}</div>
        <div class="member-sector">${m.sector}</div>
      </div>
      ${m.xaw ? `<div class="member-xaw">Expertise sollicitée ponctuellement — hors TF à proprement parler</div>` : ""}
      ${!m.xaw ? `<div class="stat-row">
        <div class="stat-box"><div class="stat-n">${opps.length}</div><div class="stat-l">Total</div></div>
        <div class="stat-box"><div class="stat-n" style="color:var(--p-fg)">${nHaute}</div><div class="stat-l">Priorité haute</div></div>
        <div class="stat-box"><div class="stat-n" style="color:var(--o-fg)">${nOpp}</div><div class="stat-l">Opportunité</div></div>
        <div class="stat-box"><div class="stat-n" style="color:var(--s-fg)">${nWatch}</div><div class="stat-l">Surveiller</div></div>
      </div>` : ""}
      ${refsHtml}
      ${opps.length ? `<div class="members-section"><div class="members-label">Opportunités positionnées</div><div class="member-opps">${oppItems}</div></div>` : `<div class="empty-state" style="padding:20px">Aucune opportunité avec ces filtres.</div>`}
    `;
    grid.appendChild(card);
  });
}

// ── VIEW 3 : MATRICES ────────────────────────────────────────────────────────
function buildMatrix(containerId, cols, getOppIndex) {
  const container = document.getElementById(containerId);
  const pcode = { haute:"P", opportunite:"O", surveiller:"S" };

  let html = `<table class="matrix"><thead><tr><th class="col-header corner"></th>`;
  cols.forEach(c => { html += `<th class="col-header">${c}</th>`; });
  html += `</tr></thead><tbody>`;

  const colCounts = new Array(cols.length).fill(0);

  MEMBERS.forEach(m => {
    html += `<tr><td class="col-member">${m.name}<span class="sector-label">${m.sector}</span></td>`;
    cols.forEach((c, ci) => {
      const oppIdx = getOppIndex(ci);
      const inOpps = m.opps.includes(oppIdx);
      if (inOpps) {
        const p = OPPS[oppIdx].priorite;
        html += `<td class="cell cell-${p}">${pcode[p]}</td>`;
        colCounts[ci]++;
      } else {
        html += `<td class="cell cell-empty">—</td>`;
      }
    });
    html += `</tr>`;
  });

  // Count row
  html += `<tr class="row-count"><td class="col-member">Membres positionnés</td>`;
  colCounts.forEach(n => { html += `<td class="cell-count">${n}</td>`; });
  html += `</tr></tbody></table>`;
  container.innerHTML = html;
}

function renderMatrice() {
  buildMatrix("matrix-domains", DOMAINS, i => i);
  buildMatrix("matrix-prescripteurs", PRESC_SHORT, i => i);
}

// ── FILTERS ──────────────────────────────────────────────────────────────────
document.querySelectorAll("#filter-pays .fbtn").forEach(btn => {
  btn.addEventListener("click", () => {
    document.querySelectorAll("#filter-pays .fbtn").forEach(b => b.classList.remove("active"));
    btn.classList.add("active");
    filterPays = btn.dataset.pays;
    renderOpps(); renderMembers();
  });
});

document.querySelectorAll("#filter-prio .fbtn").forEach(btn => {
  btn.addEventListener("click", () => {
    document.querySelectorAll("#filter-prio .fbtn").forEach(b => b.classList.remove("active"));
    btn.classList.add("active");
    filterPrio = btn.dataset.prio;
    renderOpps(); renderMembers();
  });
});

// ── TABS ─────────────────────────────────────────────────────────────────────
document.querySelectorAll(".tab").forEach(tab => {
  tab.addEventListener("click", () => {
    document.querySelectorAll(".tab").forEach(t => t.classList.remove("active"));
    document.querySelectorAll(".view").forEach(v => v.classList.remove("active"));
    tab.classList.add("active");
    document.getElementById("view-" + tab.dataset.view).classList.add("active");
  });
});

// ── INIT ─────────────────────────────────────────────────────────────────────
renderOpps();
renderMembers();
renderMatrice();
</script>
</body>
</html>
