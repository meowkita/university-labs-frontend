<script>
  import { postData } from '../../js/fetchWrapper'

  let distance = 1000
  let minutes = 1
  let seconds = 0
  let speed = 0

  function submit() {
    postData('http://localhost:8080/api/runner', { distance, time: minutes + '.' + seconds }).then(
      (data) => {
        speed = data
      }
    )
  }
</script>

<div class="container">
  <h1>Лабораторная работа №1-2</h1>
  <h3>Вычисление скорости бега</h3>
  <div>
    <table>
      <tr>
        <td>Длина дистанции:</td>
        <td><input type="text" bind:value={distance} /></td>
      </tr>
      <tr>
        <td>
          Время забега:
          <br />
          (минуты.секунды)
        </td>
        <td>
          <input type="text" bind:value={minutes} />
          <br />
          <input type="text" class="w-40" bind:value={seconds} />
        </td>
      </tr>
    </table>
  </div>
  <div />
  <div>
    <button on:click={submit}>Рассчитать</button>
    {#if speed > 0}
      <p>Скорость: <span class="color-accent">{speed}</span> км/час</p>
    {:else}
      <p>Введите данные и нажмите кнопку "Рассчитать"</p>
    {/if}
  </div>
</div>
