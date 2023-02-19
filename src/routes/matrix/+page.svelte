<script>
  import { postData } from '../../js/fetchWrapper'

  let matrixHeight = 2
  let matrixWidth = 2
  let matrix = [[], []]
  let responseMatrix

  function increaseHeight() {
    responseMatrix = undefined

    matrixHeight++
    matrix.push([])
  }

  function decreaseHeight() {
    if (matrixHeight - 1 === 0) {
      return
    }

    responseMatrix = undefined

    matrixHeight--
    matrix = matrix.slice(0, matrixHeight)
  }

  function increaseWidth() {
    responseMatrix = undefined

    matrixWidth++
  }

  function decreaseWidth() {
    if (matrixWidth - 1 === 0) {
      return
    }

    responseMatrix = undefined

    matrixWidth--
    for (let i = 0; i < matrixWidth; i++) {
      matrix[i] = matrix[i].slice(0, matrixWidth)
    }
  }

  function writeToMatrix(value, x, y) {
    matrix[x][y] = value
  }

  function submit() {
    postData('http://localhost:8080/api/matrix', { matrix }).then((data) => {
      responseMatrix = data.matrix
    })
  }
</script>

<div class="container">
  <h1>Лабораторная работа №5</h1>
  <h3>Поиск индексов с максимальным и минимальным значением и их перестановка</h3>
  <div>
    <table>
      <tr>
        <td>Высота матрицы:</td>
        <td><button on:click={increaseHeight}>+</button></td>
        <td><button on:click={decreaseHeight}>-</button></td>
        <td>Ширина матрицы:</td>
        <td><button on:click={increaseWidth}>+</button></td>
        <td><button on:click={decreaseWidth}>-</button></td>
      </tr>
    </table>
    <p />
    <table>
      {#each Array(matrixHeight) as _, x (x)}
        <tr>
          {#each Array(matrixWidth) as _, y (y)}
            <td>
              <input type="text" on:input={(event) => writeToMatrix(event.target.value, x, y)} />
            </td>
          {/each}
        </tr>
      {/each}
    </table>
  </div>
  <div>
    <button on:click={submit}>Проверить</button>
    <hr />
    {#if responseMatrix !== undefined}
      <p>Результат</p>
      <table>
        {#each Array(matrixHeight) as _, x (x)}
          <tr>
            {#each Array(matrixWidth) as _, y (y)}
              <td>
                <p>{responseMatrix[x][y]}</p>
              </td>
            {/each}
          </tr>
        {/each}
      </table>
    {:else}
      <p>Введите данные и нажмите кнопку "Рассчитать"</p>
    {/if}
  </div>
</div>
