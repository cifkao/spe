---
title: Stochastic Positional Encoding
description: 'Relative Positional Encoding for Transformers with Linear Complexity'
---

{::options toc_levels="1..3" /}

## Contents
{: .no_toc}
* TOC
{:toc}

## Examples

[MIDI file browser]({{ "/midi_browser/" | relative_url }})

### Groove continuation

<div class="tabbed-midi-player">
<div class="tabs">
  <a href="#" data-midi-url="/midi/grv2grv/ape/maj829.RB_WILSN_a.prompt.mid" class="selected">Prompt</a>
  <a href="#" data-midi-url="/midi/grv2grv/ape/maj829.RB_WILSN_a.prompt_cont_0.mid">APE</a>
  <a href="#" data-midi-url="/midi/grv2grv/sinespe/maj829.RB_WILSN_a.prompt_cont_0.mid">SineSPE</a>
  <a href="#" data-midi-url="/midi/grv2grv/convspe/maj829.RB_WILSN_a.prompt_cont_0.mid">ConvSPE</a>
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

<script>
document.querySelectorAll('midi-visualizer').forEach(function (element) {
  element.config.noteHeight = 4;
  element.config.pixelsPerTimeStep = 30;
});

document.querySelectorAll('.tabbed-midi-player').forEach(function (container) {
  const visualizer = container.querySelector('midi-visualizer');
  const player = container.querySelector('midi-player');
  const defaultUrl = container.querySelector('a[data-midi-url].selected').dataset.midiUrl;
  player.addVisualizer(visualizer);
  player.src = defaultUrl;
  visualizer.src = defaultUrl;

  container.querySelectorAll('a[data-midi-url]').forEach(function (link) {
    const url = link.dataset.midiUrl;
    link.addEventListener('click', function (event) {
      event.preventDefault();
      player.src = url;
      visualizer.src = url;
      container.querySelector('a[data-midi-url].selected').classList.remove('selected');
      link.classList.add('selected');
    });
  });
});
</script>
