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

<section id="pop-piano" markdown="1">

### Pop piano generation

The following examples are generated from models trained for pop piano generation with sequence length 2048.
We display outputs up to length 2560 to demonstrate extrapolation.
*APE* refers to the Performer model with absolute positional encoding, the rest use our proposed *sinusoidal*
and *convolutional SPE* (*gated* and *ungated* variants).
We can clearly observe that the outputs from *APE* quickly become incoherent once the training length
is exceeded (the time at which this happens depends on the tempo and style of each example).
On the other hand, SPE-based models (especially *ungated convolutional SPE*) seem to extrapolate well.

Use the following checkbox to control whether the extrapolation (beyond length 2048) is displayed or not.

<div>
<input type="checkbox" id="popExtrapolate" name="popExtrapolate" checked>
<label for="popExtrapolate" style="font-weight: bold;">Show extrapolation</label>
</div>

#### APE

<div class="tabbed-midi-player">
<div class="tabs">
  {% for num in (1..10) %}
    <a href="#" data-midi-url="/midi/pop_piano/ape/samp{{ num | prepend: '00' | slice: -2, 2 }}_extrapolation.mid">{{ num }}</a>
  {% endfor %}
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

#### Sinusoidal SPE, gated

<div class="tabbed-midi-player">
<div class="tabs">
  {% for num in (1..10) %}
    <a href="#" data-midi-url="/midi/pop_piano/sinespe/samp{{ num | prepend: '00' | slice: -2, 2 }}_extrapolation.mid">{{ num }}</a>
  {% endfor %}
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

#### Sinusoidal SPE, ungated

<div class="tabbed-midi-player">
<div class="tabs">
  {% for num in (1..10) %}
    <a href="#" data-midi-url="/midi/pop_piano/sinespe_ungated/samp{{ num | prepend: '00' | slice: -2, 2 }}_extrapolation.mid">{{ num }}</a>
  {% endfor %}
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

#### Convolutional SPE, gated

<div class="tabbed-midi-player">
<div class="tabs">
  {% for num in (1..10) %}
    <a href="#" data-midi-url="/midi/pop_piano/convspe/samp{{ num | prepend: '00' | slice: -2, 2 }}_extrapolation.mid">{{ num }}</a>
  {% endfor %}
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

#### Convolutional SPE, ungated

<div class="tabbed-midi-player">
<div class="tabs">
  {% for num in (1..10) %}
    <a href="#" data-midi-url="/midi/pop_piano/convspe_ungated/samp{{ num | prepend: '00' | slice: -2, 2 }}_extrapolation.mid">{{ num }}</a>
  {% endfor %}
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

</section>

### Groove continuation
The following examples are from models trained on the Groove2Groove accompaniment dataset.
In each example, we prompt the model with 2 bars of a new accompaniment (unseen during training) and then
let it generate a continuation. While the models were trained on segments of length 512 (corresponding to
2–10 bars), we let them generate 1024 tokens to test extrapolation.
Again, SPE-based models are clearly superior to APE-based ones in terms of the quality of the generated
samples, although the former also slightly degrade over time.

Both SPE-based models use the *gated* variant.

<div class="tabbed-midi-player">
<div class="tabs">
  <a href="#" data-midi-url="/midi/grv2grv/ape/maj357.C_SAMMY_b.prompt.mid" class="selected">Prompt</a>
  <a href="#" data-midi-url="/midi/grv2grv/ape/maj357.C_SAMMY_b.prompt_cont_0.mid">APE</a>
  <a href="#" data-midi-url="/midi/grv2grv/sinespe/maj357.C_SAMMY_b.prompt_cont_0.mid">Sinusoidal SPE</a>
  <a href="#" data-midi-url="/midi/grv2grv/convspe/maj357.C_SAMMY_b.prompt_cont_0.mid">Convolutional SPE</a>
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

<div class="tabbed-midi-player">
<div class="tabs">
  <a href="#" data-midi-url="/midi/grv2grv/ape/min114.EUROBEA3_a.prompt.mid" class="selected">Prompt</a>
  <a href="#" data-midi-url="/midi/grv2grv/ape/min114.EUROBEA3_a.prompt_cont_1.mid">APE</a>
  <a href="#" data-midi-url="/midi/grv2grv/sinespe/min114.EUROBEA3_a.prompt_cont_2.mid">Sinusoidal SPE</a>
  <a href="#" data-midi-url="/midi/grv2grv/convspe/min114.EUROBEA3_a.prompt_cont_2.mid">Convolutional SPE</a>
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

<div class="tabbed-midi-player">
<div class="tabs">
  <a href="#" data-midi-url="/midi/grv2grv/ape/min183.BuddyG_a.prompt.mid" class="selected">Prompt</a>
  <a href="#" data-midi-url="/midi/grv2grv/ape/min183.BuddyG_a.prompt_cont_0.mid">APE</a>
  <a href="#" data-midi-url="/midi/grv2grv/sinespe/min183.BuddyG_a.prompt_cont_0.mid">Sinusoidal SPE</a>
  <a href="#" data-midi-url="/midi/grv2grv/convspe/min183.BuddyG_a.prompt_cont_2.mid">Convolutional SPE</a>
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

<div class="tabbed-midi-player">
<div class="tabs">
  <a href="#" data-midi-url="/midi/grv2grv/ape/maj297.CHARLSTN_b.prompt.mid" class="selected">Prompt</a>
  <a href="#" data-midi-url="/midi/grv2grv/ape/maj297.CHARLSTN_b.prompt_cont_2.mid">APE</a>
  <a href="#" data-midi-url="/midi/grv2grv/sinespe/maj297.CHARLSTN_b.prompt_cont_1.mid">Sinusoidal SPE</a>
  <a href="#" data-midi-url="/midi/grv2grv/convspe/maj297.CHARLSTN_b.prompt_cont_2.mid">Convolutional SPE</a>
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>

<div class="tabbed-midi-player">
<div class="tabs">
  <a href="#" data-midi-url="/midi/grv2grv/ape/maj572.TekJungl_b.prompt.mid" class="selected">Prompt</a>
  <a href="#" data-midi-url="/midi/grv2grv/ape/maj572.TekJungl_b.prompt_cont_2.mid">APE</a>
  <a href="#" data-midi-url="/midi/grv2grv/sinespe/maj572.TekJungl_b.prompt_cont_2.mid">Sinusoidal SPE</a>
  <a href="#" data-midi-url="/midi/grv2grv/convspe/maj572.TekJungl_b.prompt_cont_2.mid">Convolutional SPE</a>
</div>
<midi-visualizer></midi-visualizer>
<midi-player sound-font></midi-player>
</div>


<script>
document.querySelectorAll('midi-visualizer').forEach(function (visualizer) {
  visualizer.config.noteHeight = 4;
  visualizer.config.pixelsPerTimeStep = 30;
  visualizer.classList.add('loading');
});

document.querySelectorAll('.tabbed-midi-player').forEach(function (container) {
  // Make first tab selected
  if (!container.querySelector('a[data-midi-url].selected')) {
    container.querySelector('a[data-midi-url]').classList.add('selected');
  }

  const visualizer = container.querySelector('midi-visualizer');
  const player = container.querySelector('midi-player');
  const defaultUrl = container.querySelector('a[data-midi-url].selected').dataset.midiUrl;
  player.addVisualizer(visualizer);
  player.src = defaultUrl;
  visualizer.src = defaultUrl;

  player.addEventListener('load', function() {
    visualizer.classList.remove('loading');
  });
  player.addEventListener('start', function () {
    visualizer.querySelector('.piano-roll-visualizer').scrollLeft = 0;
  });

  // Tabs
  container.querySelectorAll('a[data-midi-url]').forEach(function (link) {
    link.addEventListener('click', function (event) {
      event.preventDefault();
      player.src = link.dataset.midiUrl;
      visualizer.src = link.dataset.midiUrl;
      visualizer.classList.add('loading');
      visualizer.querySelector('.piano-roll-visualizer').scrollLeft = 0;
      container.querySelector('a[data-midi-url].selected').classList.remove('selected');
      link.classList.add('selected');
    });
  });
});

document.querySelector('#popExtrapolate').addEventListener('change', function () {
  document.querySelectorAll('#pop-piano a[data-midi-url]').forEach(function (tab) {
    if (document.querySelector('#popExtrapolate').checked) {
      if (tab.dataset.midiUrl.indexOf('_extrapolation') < 0) {
        tab.dataset.midiUrl = tab.dataset.midiUrl.replace('.mid', '_extrapolation.mid');
      }
    } else {
      tab.dataset.midiUrl = tab.dataset.midiUrl.replace('_extrapolation', '');
    }

    if (tab.classList.contains('selected')) {
      tab.click();
    }
  });
});
</script>
