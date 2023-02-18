<script>
  import { postData } from '../../js/fetchWrapper'

  let number = 0
  let isEven

  function submit() {
    postData('http://localhost:8080/api/even?number=' + number).then((data) => {
      isEven = data
    })
  }
</script>

<div class="container">
  <h1>Лабораторная работа №3</h1>
  <h3>Проверка числа на четность/нечетность</h3>
  <div>
    <table>
      <tr>
        <td>Число:</td>
        <td><input type="text" bind:value={number} /></td>
      </tr>
    </table>
  </div>
  <div />
  <div>
    <button on:click={submit}>Проверить</button>
    {#if isEven !== undefined}
      <p>Число <span class="color-accent">{isEven ? 'чётное' : 'нечётное'}</span></p>
    {:else}
      <p>Введите данные и нажмите кнопку "Рассчитать"</p>
    {/if}
  </div>
</div>
