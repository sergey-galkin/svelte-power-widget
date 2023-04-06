<script lang="ts">
  import { onDestroy, onMount } from 'svelte';
  import mqtt from 'precompiled-mqtt'
  
  const channel = 'power-app';
  let power = '50';
  let range: HTMLInputElement;
  let client: mqtt.MqttClient 
  
  onMount(() => {
    client = mqtt.connect('ws://test.mosquitto.org:8081')
    client.subscribe(channel)
    client.on("message", function (topic, payload) {
      power = payload.toString();
    })
  })
  
  onDestroy(() => client.end())

  const send = () => {
    client.publish(channel, range.value);
  }
  
</script>

<main class="container">
  <h1>Мощность:</h1>
  <div class="numValue">{power}%</div>
  <input class="range" type="range" bind:value={power} bind:this={range} min="0" max="100" on:change={send}>
</main>

<style>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    height: 100vh;
    font-family: Helvetica, Arial, sans-serif;
    font-size: 1.5em;
  }
  .numValue {
    font-size: 4em;
  }
  .range {
    width: 300px;
    margin-top: 20px;
  }
</style>