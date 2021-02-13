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
The following examples are from models trained on the Groove2Groove dataset, consisting of accompaniments.
In each example, we prompt the model with 2 bars of a new accompaniment (unseen during training) and then
let it generate a continuation. The first tab displays the initial prompt, the following tabs contain
continuations generated from the three respective models evaluated in the paper.

<div class="tabbed-midi-player">
<div class="tabs">
  <a href="#" data-midi-url="/midi/grv2grv/ape/maj357.C_SAMMY_b.prompt.mid" class="selected">Prompt</a>
  <a href="#" data-midi-url="/midi/grv2grv/ape/maj357.C_SAMMY_b.prompt_cont_0.mid">APE</a>
  <a href="#" data-midi-url="/midi/grv2grv/sinespe/maj357.C_SAMMY_b.prompt_cont_0.mid">SineSPE</a>
  <a href="#" data-midi-url="/midi/grv2grv/convspe/maj357.C_SAMMY_b.prompt_cont_0.mid">ConvSPE</a>
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

<div class="tabbed-midi-player">
<div class="tabs">
  <a href="#" data-midi-url="/midi/grv2grv/ape/min114.EUROBEA3_a.prompt.mid" class="selected">Prompt</a>
  <a href="#" data-midi-url="/midi/grv2grv/ape/min114.EUROBEA3_a.prompt_cont_1.mid">APE</a>
  <a href="#" data-midi-url="/midi/grv2grv/sinespe/min114.EUROBEA3_a.prompt_cont_2.mid">SineSPE</a>
  <a href="#" data-midi-url="/midi/grv2grv/convspe/min114.EUROBEA3_a.prompt_cont_2.mid">ConvSPE</a>
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

<div class="tabbed-midi-player">
<div class="tabs">
  <a href="#" data-midi-url="/midi/grv2grv/ape/min183.BuddyG_a.prompt.mid" class="selected">Prompt</a>
  <a href="#" data-midi-url="/midi/grv2grv/ape/min183.BuddyG_a.prompt_cont_0.mid">APE</a>
  <a href="#" data-midi-url="/midi/grv2grv/sinespe/min183.BuddyG_a.prompt_cont_0.mid">SineSPE</a>
  <a href="#" data-midi-url="/midi/grv2grv/convspe/min183.BuddyG_a.prompt_cont_2.mid">ConvSPE</a>
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

<script>
document.querySelectorAll('midi-visualizer').forEach(function (visualizer) {
  visualizer.config.noteHeight = 4;
  visualizer.config.pixelsPerTimeStep = 30;
});

document.querySelectorAll('.tabbed-midi-player').forEach(function (container) {
  const visualizer = container.querySelector('midi-visualizer');
  const player = container.querySelector('midi-player');
  const defaultUrl = container.querySelector('a[data-midi-url].selected').dataset.midiUrl;
  player.addVisualizer(visualizer);
  player.src = defaultUrl;
  visualizer.src = defaultUrl;

  player.addEventListener('start', function () {
    visualizer.querySelector('.piano-roll-visualizer').scrollLeft = 0;
  });

  // Tabs
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
