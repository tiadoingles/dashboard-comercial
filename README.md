<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Dashboard Comercial · Fluent Mind Academy</title>
  <style>
    *,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
    body{font-family:'Inter',system-ui,sans-serif;background:#f5f6fa;color:#2c3e50}
    .header{background:linear-gradient(135deg,#1a2744 0%,#2d3f6e 100%);color:#fff;padding:24px 28px 0}
    .header-top{display:flex;justify-content:space-between;flex-wrap:wrap;gap:14px;margin-bottom:18px;align-items:flex-start}
    .brand{font-size:11px;color:#4db8d4;font-weight:700;letter-spacing:2px;text-transform:uppercase}
    .title{font-size:24px;font-weight:900;margin-top:4px}
    .updated{font-size:11px;color:rgba(255,255,255,0.4);margin-top:4px}
    .filters{display:flex;align-items:center;gap:10px;flex-wrap:wrap}
    .filters label{color:rgba(255,255,255,0.7);font-size:13px;font-weight:600}
    .filters input[type=date]{border-radius:8px;border:1.5px solid rgba(255,255,255,0.25);padding:6px 10px;font-size:13px;font-weight:600;background:rgba(255,255,255,0.12);color:#fff;color-scheme:dark;cursor:pointer}
    .sep{color:rgba(255,255,255,0.45)}
    .btn-clear{background:rgba(255,255,255,0.15);border:none;border-radius:8px;padding:7px 14px;color:#fff;font-size:12px;font-weight:700;cursor:pointer}
    .fcount{color:rgba(255,255,255,0.4);font-size:12px}
    .mes-badge{background:rgba(255,255,255,0.12);border:1px solid rgba(255,255,255,0.2);border-radius:8px;padding:5px 12px;color:#4db8d4;font-size:12px;font-weight:700;display:none}
    .tabs{display:flex;gap:4px;flex-wrap:wrap}
    .tab{padding:9px 18px;border-radius:10px 10px 0 0;border:none;cursor:pointer;font-weight:700;font-size:13px;background:transparent;color:rgba(255,255,255,0.6);transition:all .2s}
    .tab.active{background:#fff}
    .tab[data-tab="geral"].active{color:#1a2744}
    .tab[data-tab="closer"].active{color:#27ae60}
    .tab[data-tab="ss"].active{color:#ea5167}
    .tab[data-tab="sdr"].active{color:#f5a623}
    .tab[data-tab="is"].active{color:#4db8d4}
    .content{padding:26px 28px}
    .panel{display:none}.panel.active{display:block}
    .section{margin-bottom:28px}
    .sec-title{display:flex;align-items:center;gap:10px;margin-bottom:14px}
    .sec-bar{width:5px;height:28px;border-radius:3px;flex-shrink:0}
    .sec-title h2{font-size:17px;font-weight:800}
    .kpi-row{display:flex;gap:14px;flex-wrap:wrap}
    .kpi{background:#fff;border-radius:14px;padding:18px 20px;box-shadow:0 2px 12px rgba(0,0,0,0.07);min-width:160px;flex:1}
    .kpi-label{font-size:11px;color:#888;font-weight:600;text-transform:uppercase;letter-spacing:1px;margin-bottom:6px;display:flex;align-items:center;gap:5px;flex-wrap:wrap}
    .kpi-value{font-size:26px;font-weight:800}
    .kpi-meta{margin-top:8px}
    .meta-row{display:flex;justify-content:space-between;font-size:11px;color:#aaa;margin-bottom:3px}
    .bar-bg{background:#eee;border-radius:99px;height:6px}
    .bar{height:6px;border-radius:99px;transition:width .6s ease}
    .cash-badge{display:inline-flex;align-items:center;gap:4px;border-radius:20px;padding:3px 10px;font-size:12px;font-weight:800;color:#fff;margin-top:8px}
    .warn{cursor:help;position:relative;display:inline-flex;align-items:center;font-size:14px;flex-shrink:0}
    .warn .tip{display:none;position:absolute;bottom:calc(100% + 7px);left:50%;transform:translateX(-50%);background:#222;color:#fff;font-size:11px;font-weight:400;padding:6px 10px;border-radius:8px;white-space:nowrap;z-index:99;text-transform:none;letter-spacing:0;pointer-events:none;box-shadow:0 4px 12px rgba(0,0,0,0.3)}
    .warn .tip::after{content:'';position:absolute;top:100%;left:50%;transform:translateX(-50%);border:5px solid transparent;border-top-color:#222}
    .warn:hover .tip{display:block}
    .stat-row{display:flex;gap:14px;flex-wrap:wrap}
    .stat{background:#fff;border-radius:14px;padding:18px 22px;box-shadow:0 2px 12px rgba(0,0,0,0.07);flex:1;min-width:160px}
    .stat-label{font-size:11px;color:#888;font-weight:600;text-transform:uppercase;letter-spacing:1px;margin-bottom:4px}
    .stat-value{font-size:30px;font-weight:900}
    .stat-desc{font-size:11px;color:#bbb;margin-top:2px}
    .chart-wrap{background:#fff;border-radius:14px;padding:20px 24px;box-shadow:0 2px 12px rgba(0,0,0,0.06)}
    .chart{display:flex;align-items:flex-end;gap:3px;height:150px;padding-top:10px}
    .chart-col{flex:1;display:flex;flex-direction:column;align-items:center;gap:2px;min-width:0}
    .chart-val{font-size:8px;color:#888;font-weight:600;white-space:nowrap}
    .chart-bar{width:100%;border-radius:4px 4px 0 0;min-height:2px;opacity:.85}
    .chart-lbl{font-size:7px;color:#aaa;text-align:center;transform:rotate(-40deg);transform-origin:top center;margin-top:4px;white-space:nowrap}
    .table-wrap{background:#fff;border-radius:14px;overflow:auto;box-shadow:0 2px 12px rgba(0,0,0,0.06)}
    table{width:100%;border-collapse:collapse;font-size:13px}
    thead tr{color:#fff}
    th{padding:10px 13px;text-align:left;font-weight:700;white-space:nowrap}
    td{padding:9px 13px;white-space:nowrap}
    .loading{display:flex;align-items:center;justify-content:center;height:300px;font-size:16px;color:#aaa;flex-direction:column;gap:12px}
    .spinner{width:36px;height:36px;border:4px solid #eee;border-top-color:#ea5167;border-radius:50%;animation:spin .8s linear infinite}
    @keyframes spin{to{transform:rotate(360deg)}}
    .footer{text-align:center;color:#bbb;font-size:11px;margin-top:16px}
    .stars{color:#f5a623}
  </style>
</head>
<body>
<div class="header">
  <div class="header-top">
    <div>
      <div class="brand">Fluent Mind Academy</div>
      <div class="title">Dashboard Comercial 📊</div>
      <div class="updated" id="last-updated">Carregando dados...</div>
    </div>
    <div class="filters">
      <label>📅 De:</label><input type="date" id="date-from"/>
      <span class="sep">até</span><input type="date" id="date-to"/>
      <button class="btn-clear" onclick="clearDates()">↺ Limpar</button>
      <span class="fcount" id="fcount"></span>
      <span class="mes-badge" id="mes-badge"></span>
    </div>
  </div>
  <div class="tabs">
    <button class="tab active" data-tab="geral"  onclick="switchTab(this)">🏠 Geral</button>
    <button class="tab"        data-tab="closer" onclick="switchTab(this)">🏆 Closer</button>
    <button class="tab"        data-tab="ss"     onclick="switchTab(this)">📲 Social Seller</button>
    <button class="tab"        data-tab="sdr"    onclick="switchTab(this)">📞 SDR</button>
    <button class="tab"        data-tab="is"     onclick="switchTab(this)">💼 Inside Sales</button>
  </div>
</div>
<div class="content">
  <div id="loading" class="loading"><div class="spinner"></div><span>Carregando dados...</span></div>

  <!-- GERAL -->
  <div class="panel active" id="panel-geral">
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#1a2744"></div><h2>Visão Geral</h2></div>
      <div class="kpi-row">
        <div class="kpi" style="border-top:4px solid #1a2744"><div class="kpi-label">💰 Faturamento Total</div><div class="kpi-value" id="g-fat">—</div></div>
        <div class="kpi" style="border-top:4px solid #1a2744"><div class="kpi-label">💵 Cash Collected Total</div><div class="kpi-value" id="g-cash">—</div><div id="g-cash-badge"></div></div>
        <div class="kpi" style="border-top:4px solid #ea5167"><div class="kpi-label">📲 Ativações SS</div><div class="kpi-value" id="g-ss-atv">—</div><div class="kpi-meta" id="g-ss-atv-meta"></div></div>
        <div class="kpi" style="border-top:4px solid #f5a623"><div class="kpi-label">📅 Agendamentos SDR</div><div class="kpi-value" id="g-sdr-agend">—</div><div class="kpi-meta" id="g-sdr-agend-meta"></div></div>
        <div class="kpi" style="border-top:4px solid #27ae60"><div class="kpi-label">🏆 Vendas Closer</div><div class="kpi-value" id="g-cl-vendas">—</div><div class="kpi-meta" id="g-cl-vendas-meta"></div></div>
        <div class="kpi" style="border-top:4px solid #4db8d4"><div class="kpi-label">💼 Vendas Inside Sales</div><div class="kpi-value" id="g-is-vendas">—</div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#f5a623"></div><h2>Taxas de Conversão</h2></div>
      <div class="stat-row">
        <div class="stat" style="border-top:4px solid #27ae60"><div class="stat-label">Taxa de Show (Closer)</div><div class="stat-value" style="color:#27ae60" id="g-show-rate">—</div><div class="stat-desc">Agendadas → Realizadas</div></div>
        <div class="stat" style="border-top:4px solid #27ae60"><div class="stat-label">Taxa Fechamento (Closer)</div><div class="stat-value" style="color:#27ae60" id="g-close-rate">—</div><div class="stat-desc">Realizadas → Vendas</div></div>
        <div class="stat" style="border-top:4px solid #f5a623"><div class="stat-label">Taxa Atend. SDR</div><div class="stat-value" style="color:#f5a623" id="g-sdr-atend-rate">—</div><div class="stat-desc">Ligações → Atendidas</div></div>
        <div class="stat" style="border-top:4px solid #ea5167"><div class="stat-label">Conv. SS → Lead</div><div class="stat-value" style="color:#ea5167" id="g-ss-conv">—</div><div class="stat-desc">Ativações → Leads SDR</div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#27ae60"></div><h2>Faturamento por Dia</h2></div>
      <div class="chart-wrap"><div class="chart" id="chart-geral"></div></div>
    </div>
  </div>

  <!-- CLOSER -->
  <div class="panel" id="panel-closer">
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#27ae60"></div><h2>Closer — Performance</h2></div>
      <div class="kpi-row">
        <div class="kpi" style="border-top:4px solid #27ae60"><div class="kpi-label">📅 Calls Agendadas</div><div class="kpi-value" id="cl-agend">—</div><div class="kpi-meta" id="cl-agend-meta"></div></div>
        <div class="kpi" style="border-top:4px solid #27ae60"><div class="kpi-label">✅ Calls Realizadas</div><div class="kpi-value" id="cl-real">—</div><div class="kpi-meta" id="cl-real-meta"></div></div>
        <div class="kpi" style="border-top:4px solid #ea5167"><div class="kpi-label">❌ No-Show <small style="font-size:10px;text-transform:none;font-weight:400">(agend − realiz.)</small></div><div class="kpi-value" id="cl-noshow">—</div><div class="kpi-meta" id="cl-noshow-meta"></div></div>
        <div class="kpi" style="border-top:4px solid #f5a623"><div class="kpi-label">🏆 Nº de Vendas</div><div class="kpi-value" id="cl-vendas">—</div><div class="kpi-meta" id="cl-vendas-meta"></div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#27ae60"></div><h2>Financeiro — Closer</h2></div>
      <div class="kpi-row">
        <div class="kpi" style="border-top:4px solid #27ae60"><div class="kpi-label">💰 Faturamento Total</div><div class="kpi-value" id="cl-fat">—</div><div class="kpi-meta" id="cl-fat-meta"></div></div>
        <div class="kpi" style="border-top:4px solid #27ae60"><div class="kpi-label">🎯 Ticket Médio</div><div class="kpi-value" id="cl-ticket">—</div></div>
        <div class="kpi" style="border-top:4px solid #27ae60"><div class="kpi-label">💵 Cash Collected</div><div class="kpi-value" id="cl-cash">—</div><div id="cl-cash-badge"></div><div class="kpi-meta" id="cl-cash-meta"></div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#27ae60"></div><h2>Taxas</h2></div>
      <div class="stat-row">
        <div class="stat" style="border-top:4px solid #27ae60"><div class="stat-label">Taxa de Show</div><div class="stat-value" style="color:#27ae60" id="cl-show-rate">—</div><div class="stat-desc">Agendadas → Realizadas</div></div>
        <div class="stat" style="border-top:4px solid #27ae60"><div class="stat-label">Taxa de Fechamento</div><div class="stat-value" style="color:#27ae60" id="cl-close-rate">—</div><div class="stat-desc">Realizadas → Vendas</div></div>
        <div class="stat" style="border-top:4px solid #ea5167"><div class="stat-label">Taxa No-Show %</div><div class="stat-value" style="color:#ea5167" id="cl-noshow-rate">—</div><div class="stat-desc">% das agendadas</div></div>
        <div class="stat" style="border-top:4px solid #f5a623"><div class="stat-label">Em Negociação</div><div class="stat-value" style="color:#f5a623" id="cl-neg">—</div></div>
        <div class="stat" style="border-top:4px solid #ea5167"><div class="stat-label">Recusou</div><div class="stat-value" style="color:#ea5167" id="cl-rec">—</div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#27ae60"></div><h2>Faturamento por Dia</h2></div>
      <div class="chart-wrap"><div class="chart" id="chart-closer"></div></div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#27ae60"></div><h2>Histórico Diário</h2></div>
      <div class="table-wrap"><table><thead><tr style="background:#27ae60"><th>Dia</th><th>Data</th><th>Agend.</th><th>Realiz.</th><th>No-Show</th><th>Vendas</th><th>Neg.</th><th>Recusou</th><th>Faturamento</th><th>Cash</th></tr></thead><tbody id="tbody-closer"></tbody></table></div>
    </div>
  </div>

  <!-- SOCIAL SELLER -->
  <div class="panel" id="panel-ss">
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#ea5167"></div><h2>Social Seller — Ativação</h2></div>
      <div class="kpi-row">
        <div class="kpi" style="border-top:4px solid #ea5167"><div class="kpi-label">📲 Ativações</div><div class="kpi-value" id="ss-atv">—</div><div class="kpi-meta" id="ss-atv-meta"></div></div>
        <div class="kpi" style="border-top:4px solid #ea5167"><div class="kpi-label">🎯 Leads Convertidos SDR</div><div class="kpi-value" id="ss-lead">—</div><div class="kpi-meta" id="ss-lead-meta"></div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#ea5167"></div><h2>Qualificação de Leads ⭐</h2></div>
      <div class="kpi-row">
        <div class="kpi" style="border-top:4px solid #f5a623"><div class="kpi-label"><span class="stars">⭐⭐⭐⭐</span>&nbsp;4 Características&nbsp;<span class="warn">⚠️<span class="tip">Meta não cadastrada para este indicador</span></span></div><div class="kpi-value" id="ss-q4">—</div></div>
        <div class="kpi" style="border-top:4px solid #f5a623"><div class="kpi-label"><span class="stars">⭐⭐⭐</span>&nbsp;3 Características&nbsp;<span class="warn">⚠️<span class="tip">Meta não cadastrada para este indicador</span></span></div><div class="kpi-value" id="ss-q3">—</div></div>
        <div class="kpi" style="border-top:4px solid #f5a623"><div class="kpi-label"><span class="stars">⭐⭐</span>&nbsp;2 Características&nbsp;<span class="warn">⚠️<span class="tip">Meta não cadastrada para este indicador</span></span></div><div class="kpi-value" id="ss-q2">—</div></div>
        <div class="kpi" style="border-top:4px solid #f5a623"><div class="kpi-label"><span class="stars">⭐</span>&nbsp;1 Característica&nbsp;<span class="warn">⚠️<span class="tip">Meta não cadastrada para este indicador</span></span></div><div class="kpi-value" id="ss-q1">—</div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#ea5167"></div><h2>Ativações por Dia</h2></div>
      <div class="chart-wrap"><div class="chart" id="chart-ss"></div></div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#ea5167"></div><h2>Histórico Diário</h2></div>
      <div class="table-wrap"><table><thead><tr style="background:#ea5167"><th>Dia</th><th>Data</th><th>Ativações</th><th>Leads SDR</th><th>⭐⭐⭐⭐</th><th>⭐⭐⭐</th><th>⭐⭐</th><th>⭐</th></tr></thead><tbody id="tbody-ss"></tbody></table></div>
    </div>
  </div>

  <!-- SDR -->
  <div class="panel" id="panel-sdr">
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#f5a623"></div><h2>SDR — Qualificação</h2></div>
      <div class="kpi-row">
        <div class="kpi" style="border-top:4px solid #f5a623"><div class="kpi-label">📞 Ligações Realizadas</div><div class="kpi-value" id="sdr-lig">—</div><div class="kpi-meta" id="sdr-lig-meta"></div></div>
        <div class="kpi" style="border-top:4px solid #f5a623"><div class="kpi-label">✅ Ligações Atendidas</div><div class="kpi-value" id="sdr-atend">—</div><div class="kpi-meta" id="sdr-atend-meta"></div></div>
        <div class="kpi" style="border-top:4px solid #f5a623"><div class="kpi-label">📅 Agendamentos</div><div class="kpi-value" id="sdr-agend">—</div><div class="kpi-meta" id="sdr-agend-meta"></div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#f5a623"></div><h2>Taxas SDR</h2></div>
      <div class="stat-row">
        <div class="stat" style="border-top:4px solid #f5a623"><div class="stat-label">Taxa Atendimento</div><div class="stat-value" style="color:#f5a623" id="sdr-taxa-atend">—</div><div class="stat-desc">Realizadas → Atendidas</div></div>
        <div class="stat" style="border-top:4px solid #f5a623"><div class="stat-label">Conv. Atend → Agend</div><div class="stat-value" style="color:#f5a623" id="sdr-taxa-agend">—</div><div class="stat-desc">Atendidas → Agendamentos</div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#f5a623"></div><h2>Ligações por Dia</h2></div>
      <div class="chart-wrap"><div class="chart" id="chart-sdr"></div></div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#f5a623"></div><h2>Histórico Diário</h2></div>
      <div class="table-wrap"><table><thead><tr style="background:#f5a623"><th>Dia</th><th>Data</th><th>Lig. Realizadas</th><th>Lig. Atendidas</th><th>Agendamentos</th></tr></thead><tbody id="tbody-sdr"></tbody></table></div>
    </div>
  </div>

  <!-- INSIDE SALES -->
  <div class="panel" id="panel-is">
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#4db8d4"></div><h2>Inside Sales — Performance</h2></div>
      <div class="kpi-row">
        <div class="kpi" style="border-top:4px solid #4db8d4"><div class="kpi-label">📞 Ligações Realizadas&nbsp;<span class="warn">⚠️<span class="tip">Meta não cadastrada na aba Metas</span></span></div><div class="kpi-value" id="is-lig-real">—</div></div>
        <div class="kpi" style="border-top:4px solid #4db8d4"><div class="kpi-label">✅ Ligações Atendidas&nbsp;<span class="warn">⚠️<span class="tip">Meta não cadastrada na aba Metas</span></span></div><div class="kpi-value" id="is-lig-atend">—</div></div>
        <div class="kpi" style="border-top:4px solid #4db8d4"><div class="kpi-label">🏆 Nº de Vendas&nbsp;<span class="warn">⚠️<span class="tip">Meta não cadastrada na aba Metas</span></span></div><div class="kpi-value" id="is-vendas">—</div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#4db8d4"></div><h2>Financeiro — Inside Sales</h2></div>
      <div class="kpi-row">
        <div class="kpi" style="border-top:4px solid #4db8d4"><div class="kpi-label">💰 Faturamento Total&nbsp;<span class="warn">⚠️<span class="tip">Meta não cadastrada na aba Metas</span></span></div><div class="kpi-value" id="is-fat">—</div></div>
        <div class="kpi" style="border-top:4px solid #4db8d4"><div class="kpi-label">🎯 Ticket Médio</div><div class="kpi-value" id="is-ticket">—</div></div>
        <div class="kpi" style="border-top:4px solid #4db8d4"><div class="kpi-label">💵 Cash Collected&nbsp;<span class="warn">⚠️<span class="tip">Meta não cadastrada na aba Metas</span></span></div><div class="kpi-value" id="is-cash">—</div><div id="is-cash-badge"></div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#4db8d4"></div><h2>Taxas</h2></div>
      <div class="stat-row">
        <div class="stat" style="border-top:4px solid #4db8d4"><div class="stat-label">Taxa Atendimento</div><div class="stat-value" style="color:#4db8d4" id="is-taxa-atend">—</div><div class="stat-desc">Realizadas → Atendidas</div></div>
        <div class="stat" style="border-top:4px solid #4db8d4"><div class="stat-label">Taxa Conversão</div><div class="stat-value" style="color:#4db8d4" id="is-taxa-conv">—</div><div class="stat-desc">Atendidas → Vendas</div></div>
      </div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#4db8d4"></div><h2>Faturamento por Dia</h2></div>
      <div class="chart-wrap"><div class="chart" id="chart-is"></div></div>
    </div>
    <div class="section">
      <div class="sec-title"><div class="sec-bar" style="background:#4db8d4"></div><h2>Histórico Diário</h2></div>
      <div class="table-wrap"><table><thead><tr style="background:#4db8d4"><th>Dia</th><th>Data</th><th>Lig. Real.</th><th>Lig. Atend.</th><th>Vendas</th><th>Faturamento</th><th>Cash</th></tr></thead><tbody id="tbody-is"></tbody></table></div>
    </div>
  </div>

  <div class="footer">Fluent Mind Academy · Dashboard Comercial · Atualização automática via Apps Script</div>
</div>

<script>
// ── SUPABASE CONFIG (seu projeto original) ────────────────────
const SUPABASE_URL='https://znazewysjyssjuqmasea.supabase.co';
const SUPABASE_ANON='eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InpuYXpld3lzanlzc2p1cW1hc2VhIiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODE2Mzg1NTUsImV4cCI6MjA5NzIxNDU1NX0.KgObQOJXiA_vvIU996fMJqTNUxxklnvA0NC5StVLnV8

';
// ATENÇÃO: substitua SUPABASE_ANON pela anon key do seu projeto em:
// https://supabase.com/dashboard/project/znazewysjyssjuqmasea/settings/api

const fmt=v=>(parseFloat(v)||0).toLocaleString('pt-BR',{style:'currency',currency:'BRL'});
const pct=(v,t)=>t>0?Math.round((v/t)*100):0;
const num=v=>(parseFloat(v)||0).toLocaleString('pt-BR');
const $=id=>document.getElementById(id);
const isoToBR=s=>s?s.split('-').reverse().join('/'):'';

function cashColor(p){return p>85?'#27ae60':p>=71?'#f5a623':'#ea5167'}
function cashEmoji(p){return p>85?'🟢':p>=71?'🟡':'🔴'}
function setCashBadge(cash,fat,elId){const p=pct(cash,fat),el=$(elId);if(!el)return;el.innerHTML=fat>0?`<div class="cash-badge" style="background:${cashColor(p)}">${cashEmoji(p)} ${p}% do faturado</div>`:'';}
function barColor(p){return p>=100?'#27ae60':p>=70?'#f5a623':'#ea5167'}
function metaHtml(value,meta,isMonetary){
  if(meta===null||meta===undefined)return'';
  const p=pct(value,meta),c=barColor(p);
  return`<div class="kpi-meta"><div class="meta-row"><span>Meta: ${isMonetary?fmt(meta):num(meta)}</span><span style="color:${c};font-weight:700">${p}%</span></div><div class="bar-bg"><div class="bar" style="background:${c};width:${Math.min(p,100)}%"></div></div></div>`;
}

// Estado global
let allData=[],filtered=[],metasMap={},minDate='',maxDate='';

function getMesKey(filtered){
  if(!filtered.length)return null;
  const counts={};
  filtered.forEach(d=>{if(!d.date)return;const p=d.date.split('-');const k=p[1]+'.'+p[0].slice(2);counts[k]=(counts[k]||0)+1;});
  return Object.keys(counts).sort((a,b)=>counts[b]-counts[a])[0]||null;
}

function switchTab(btn){
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  btn.classList.add('active');$('panel-'+btn.dataset.tab).classList.add('active');
}

function applyFilter(){
  const from=$('date-from').value||minDate,to=$('date-to').value||maxDate;
  filtered=allData.filter(d=>d.date>=from&&d.date<=to);
  $('fcount').textContent=filtered.length+' dia'+(filtered.length!==1?'s':'');
  const mk=getMesKey(filtered),mb=$('mes-badge');
  if(mk){mb.textContent='📊 Meta: '+mk;mb.style.display='inline';}else{mb.style.display='none';}
  render();
}
function clearDates(){$('date-from').value=minDate;$('date-to').value=maxDate;applyFilter();}
$('date-from').addEventListener('change',applyFilter);
$('date-to').addEventListener('change',applyFilter);
const sum=key=>filtered.reduce((a,d)=>a+(parseFloat(d[key])||0),0);

function render(){
  const mk=getMesKey(filtered);
  const M=metasMap[mk]||{};

  const cl_agend=sum('closer_agend'),cl_real=sum('closer_real'),cl_noshow=cl_agend-cl_real;
  const cl_vendas=sum('closer_vendas'),cl_fat=sum('closer_fat'),cl_cash=sum('closer_cash');
  const cl_neg=sum('closer_neg'),cl_rec=sum('closer_rec');
  const cl_ticket=cl_vendas>0?cl_fat/cl_vendas:0;
  const cl_ns_pct=pct(cl_noshow,cl_agend);
  const ss_atv=sum('ss_atv'),ss_lead=sum('ss_lead');
  const ss_q1=sum('ss_q1'),ss_q2=sum('ss_q2'),ss_q3=sum('ss_q3'),ss_q4=sum('ss_q4');
  const sdr_lig=sum('sdr_lig'),sdr_atend=sum('sdr_atend'),sdr_agend=sum('sdr_agend');
  const is_lig_real=sum('is_lig_real'),is_lig_atend=sum('is_lig_atend');
  const is_vendas=sum('is_vendas'),is_fat=sum('is_fat'),is_cash=sum('is_cash');
  const is_ticket=is_vendas>0?is_fat/is_vendas:0;
  const totalFat=cl_fat+is_fat+sum('sdr_fat'),totalCash=cl_cash+is_cash+sum('sdr_cash');

  // GERAL
  $('g-fat').textContent=fmt(totalFat);$('g-cash').textContent=fmt(totalCash);setCashBadge(totalCash,totalFat,'g-cash-badge');
  $('g-ss-atv').textContent=num(ss_atv);$('g-ss-atv-meta').innerHTML=metaHtml(ss_atv,M.ss_atv,false);
  $('g-sdr-agend').textContent=num(sdr_agend);$('g-sdr-agend-meta').innerHTML=metaHtml(sdr_agend,M.sdr_agend,false);
  $('g-cl-vendas').textContent=num(cl_vendas);$('g-cl-vendas-meta').innerHTML=metaHtml(cl_vendas,M.closer_vendas,false);
  $('g-is-vendas').textContent=num(is_vendas);
  $('g-show-rate').textContent=pct(cl_real,cl_agend)+'%';$('g-close-rate').textContent=pct(cl_vendas,cl_real)+'%';
  $('g-sdr-atend-rate').textContent=pct(sdr_atend,sdr_lig)+'%';$('g-ss-conv').textContent=pct(ss_lead,ss_atv)+'%';

  // CLOSER
  $('cl-agend').textContent=num(cl_agend);$('cl-agend-meta').innerHTML=metaHtml(cl_agend,M.closer_agend,false);
  $('cl-real').textContent=num(cl_real);$('cl-real-meta').innerHTML=metaHtml(cl_real,M.closer_real,false);
  $('cl-noshow').textContent=num(cl_noshow);
  if(M.closer_noshow_pct!=null){const ok=cl_ns_pct<=M.closer_noshow_pct,c=ok?'#27ae60':'#ea5167';$('cl-noshow-meta').innerHTML=`<div class="kpi-meta"><div class="meta-row"><span>Meta máx: ${M.closer_noshow_pct}%</span><span style="color:${c};font-weight:700">${cl_ns_pct}% ${ok?'✅':'⚠️'}</span></div></div>`;}
  else $('cl-noshow-meta').innerHTML='';
  $('cl-vendas').textContent=num(cl_vendas);$('cl-vendas-meta').innerHTML=metaHtml(cl_vendas,M.closer_vendas,false);
  $('cl-fat').textContent=fmt(cl_fat);$('cl-fat-meta').innerHTML=metaHtml(cl_fat,M.closer_fat,true);
  $('cl-ticket').textContent=fmt(cl_ticket);
  $('cl-cash').textContent=fmt(cl_cash);setCashBadge(cl_cash,cl_fat,'cl-cash-badge');$('cl-cash-meta').innerHTML=metaHtml(cl_cash,M.closer_cash,true);
  $('cl-show-rate').textContent=pct(cl_real,cl_agend)+'%';$('cl-close-rate').textContent=pct(cl_vendas,cl_real)+'%';
  $('cl-noshow-rate').textContent=cl_ns_pct+'%';$('cl-neg').textContent=num(cl_neg);$('cl-rec').textContent=num(cl_rec);

  // SS
  $('ss-atv').textContent=num(ss_atv);$('ss-atv-meta').innerHTML=metaHtml(ss_atv,M.ss_atv,false);
  $('ss-lead').textContent=num(ss_lead);$('ss-lead-meta').innerHTML=metaHtml(ss_lead,M.ss_lead,false);
  $('ss-q4').textContent=num(ss_q4);$('ss-q3').textContent=num(ss_q3);$('ss-q2').textContent=num(ss_q2);$('ss-q1').textContent=num(ss_q1);

  // SDR
  $('sdr-lig').textContent=num(sdr_lig);$('sdr-lig-meta').innerHTML=metaHtml(sdr_lig,M.sdr_lig,false);
  $('sdr-atend').textContent=num(sdr_atend);$('sdr-atend-meta').innerHTML=metaHtml(sdr_atend,M.sdr_atend,false);
  $('sdr-agend').textContent=num(sdr_agend);$('sdr-agend-meta').innerHTML=metaHtml(sdr_agend,M.sdr_agend,false);
  $('sdr-taxa-atend').textContent=pct(sdr_atend,sdr_lig)+'%';$('sdr-taxa-agend').textContent=pct(sdr_agend,sdr_atend)+'%';

  // IS
  $('is-lig-real').textContent=num(is_lig_real);$('is-lig-atend').textContent=num(is_lig_atend);
  $('is-vendas').textContent=num(is_vendas);$('is-fat').textContent=fmt(is_fat);
  $('is-ticket').textContent=fmt(is_ticket);$('is-cash').textContent=fmt(is_cash);setCashBadge(is_cash,is_fat,'is-cash-badge');
  $('is-taxa-atend').textContent=pct(is_lig_atend,is_lig_real)+'%';$('is-taxa-conv').textContent=pct(is_vendas,is_lig_atend)+'%';

  // CHARTS
  renderChart('chart-geral',d=>parseFloat(d.closer_fat)||0,'#27ae60');
  renderChart('chart-closer',d=>parseFloat(d.closer_fat)||0,'#27ae60');
  renderChart('chart-ss',d=>parseInt(d.ss_atv)||0,'#ea5167');
  renderChart('chart-sdr',d=>parseInt(d.sdr_lig)||0,'#f5a623');
  renderChart('chart-is',d=>parseFloat(d.is_fat)||0,'#4db8d4');

  // TABLES
  $('tbody-closer').innerHTML=filtered.map((d,i)=>`<tr style="background:${i%2===0?'#fff':'#f0fdf4'};border-bottom:1px solid #e0f0e8"><td style="color:#666">${d.day||''}</td><td style="font-weight:600">${isoToBR(d.date)}</td><td>${d.closer_agend||0}</td><td style="font-weight:700;color:#27ae60">${d.closer_real||0}</td><td style="color:${((d.closer_agend||0)-(d.closer_real||0))>0?'#ea5167':'#aaa'}">${(d.closer_agend||0)-(d.closer_real||0)}</td><td style="font-weight:700;color:#f5a623">${d.closer_vendas||0}</td><td>${d.closer_neg||0}</td><td style="color:#ea5167">${d.closer_rec||0}</td><td style="color:#27ae60">${fmt(d.closer_fat)}</td><td style="color:#27ae60">${fmt(d.closer_cash)}</td></tr>`).join('');
  $('tbody-ss').innerHTML=filtered.map((d,i)=>`<tr style="background:${i%2===0?'#fff':'#fef6f7'};border-bottom:1px solid #f0e0e3"><td style="color:#666">${d.day||''}</td><td style="font-weight:600">${isoToBR(d.date)}</td><td style="font-weight:700;color:#ea5167">${d.ss_atv||0}</td><td>${d.ss_lead||0}</td><td>${d.ss_q4||0}</td><td>${d.ss_q3||0}</td><td>${d.ss_q2||0}</td><td>${d.ss_q1||0}</td></tr>`).join('');
  $('tbody-sdr').innerHTML=filtered.map((d,i)=>`<tr style="background:${i%2===0?'#fff':'#fffbf0'};border-bottom:1px solid #f0e8d0"><td style="color:#666">${d.day||''}</td><td style="font-weight:600">${isoToBR(d.date)}</td><td style="font-weight:700;color:#f5a623">${d.sdr_lig||0}</td><td>${d.sdr_atend||0}</td><td>${d.sdr_agend||0}</td></tr>`).join('');
  $('tbody-is').innerHTML=filtered.map((d,i)=>`<tr style="background:${i%2===0?'#fff':'#f0fafd'};border-bottom:1px solid #e0f0f5"><td style="color:#666">${d.day||''}</td><td style="font-weight:600">${isoToBR(d.date)}</td><td style="font-weight:700;color:#4db8d4">${d.is_lig_real||0}</td><td>${d.is_lig_atend||0}</td><td style="font-weight:700;color:#f5a623">${d.is_vendas||0}</td><td style="color:#27ae60">${fmt(d.is_fat)}</td><td style="color:#27ae60">${fmt(d.is_cash)}</td></tr>`).join('');
}

function renderChart(elId,accessor,color){
  const el=$(elId);if(!el)return;
  const vals=filtered.map(accessor),max=Math.max(...vals,1),H=118;
  el.innerHTML=filtered.map((d,i)=>{const v=vals[i],h=Math.max(Math.round((v/max)*H),2),lbl=d.date?d.date.slice(5).split('-').reverse().join('/'):'',label=v>999?(v/1000).toFixed(1)+'k':v;return`<div class="chart-col"><div class="chart-val">${label}</div><div class="chart-bar" style="height:${h}px;background:${color}"></div><div class="chart-lbl">${lbl}</div></div>`;}).join('');
}

async function fetchSupabase(path){
  const res=await fetch(SUPABASE_URL+path,{headers:{'apikey':SUPABASE_ANON,'Authorization':'Bearer '+SUPABASE_ANON}});
  if(!res.ok)throw new Error('HTTP '+res.status+' em '+path);
  return res.json();
}

async function loadData(){
  try{
    // Carrega dados e metas em paralelo
    const [dados,metas]=await Promise.all([
      fetchSupabase('/rest/v1/dados_comerciais?select=*&order=date.asc&limit=2000'),
      fetchSupabase('/rest/v1/metas?select=*').catch(()=>[])
    ]);

    // Monta mapa de metas: { "08.26": { ss_atv:1365, ... } }
    metasMap={};
    metas.forEach(m=>{ if(m.mes) metasMap[m.mes]=m; });

    allData=dados;
    if(!allData.length){$('loading').innerHTML='<div style="color:#aaa;text-align:center">📭 Nenhum dado ainda.<br><small>Execute o Apps Script para sincronizar.</small></div>';return;}

    const dates=allData.map(d=>d.date).filter(Boolean).sort();
    minDate=dates[0];maxDate=dates[dates.length-1];
    ['date-from','date-to'].forEach(id=>{$(id).min=minDate;$(id).max=maxDate;});
    $('date-from').value=minDate;$('date-to').value=maxDate;

    const ult=allData[allData.length-1];
    if(ult&&ult.atualizado_em){const d=new Date(ult.atualizado_em);$('last-updated').textContent='🔄 Atualizado em: '+d.toLocaleDateString('pt-BR')+' às '+d.toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'});}

    $('loading').style.display='none';
    filtered=[...allData];$('fcount').textContent=filtered.length+' dias';
    applyFilter();
  }catch(e){$('loading').innerHTML=`<div style="color:#ea5167;font-size:14px">⚠️ Erro ao conectar<br><small style="color:#aaa">${e.message}</small></div>`;}
}
loadData();
</script>
</body>
</html>
