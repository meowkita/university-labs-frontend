<script>
  import { postData } from '../../js/fetchWrapper'

  let firstArrayString
  let secondArrayString
  let resultArray

  function submit() {
    if (firstArrayString.length === 0 || secondArrayString.length === 0) {
      return
    }

    const firstArray = firstArrayString.split(',')
    const secondArray = secondArrayString.split(',')

    postData('http://localhost:8080/api/array', { first: firstArray, second: secondArray }).then(
      (data) => {
        resultArray = data
      }
    )
  }
</script>

<div class="container">
  <h1>Лабораторная работа №4</h1>
  <h3>Объединение двух массивов в один</h3>
  <div>
    <table>
      <tr>
        <td>Первый массив:</td>
        <td><input type="text" bind:value={firstArrayString} /></td>
      </tr>
      <tr>
        <td>Второй массив:</td>
        <td><input type="text" bind:value={secondArrayString} /></td>
      </tr>
    </table>
  </div>
  <div />
  <div>
    <button on:click={submit}>Объединить</button>
    {#if resultArray !== undefined}
      <p>Результат: <span class="color-accent">{resultArray}</span></p>
    {:else}
      <p>Введите данные и нажмите кнопку "Рассчитать"</p>
    {/if}
  </div>
</div>
