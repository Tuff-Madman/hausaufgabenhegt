<script>
  import "bulma/css/bulma.css";
  let weekdays = ["Montag", "Dienstag", "Mittwoch", "Donnerstag", "Freitag"];
  let subjects = ["Deutsch", "Englisch", "Mathe", "Informatik", "Religion"];
  let tasks = [];
  let newTask = {
    weekday: "Montag",
    subject: "Deutsch",
    task: "",
    status: "offen"
  };
  let visible = false;

  function toggleVisible() {
    visible = !visible;
  }
  function weekdayTasks(weekday, tasks) {
    return tasks.filter(task => task.weekday == weekday);
  }
  function addTask() {
    tasks = [
      ...tasks,
      {
        id: tasks.length + 1,
        weekday: newTask.weekday,
        subject: newTask.subject,
        task: newTask.task,
        status: newTask.status
      }
    ];

    resetForm();
  }
  function resetForm() {
    newTask = {
      weekday: "Montag",
      subject: "Deutsch",
      task: "",
      status: "offen"
    };
  }
</script>
<style>
</style>
<header class="hero is-warning">
<div class="hero-body">
<div class="container">
<h1 class="title">
Digitales Hausaufgabenheft
</h1>
</div>
</div>
</header>
<main class="section">
<div class="container content">
<button on:click={toggleVisible} class="button is-rounded">Neue Aufgabe(n) hinzufügen</button>
{#if visible}
<form on:submit|preventDefault={addTask} on:reset|preventDefault={resetForm}>
<div class="field is-horizontal">
<div class="field-label is-normal">
<label class="label">Wochentag</label>
</div>
<div class="field-body">
<div class="field">
<div class="control">
<div class="select">
<select bind:value="{newTask.weekday}">
{#each weekdays as weekday}
<option>{weekday}</option>
{/each}
</select>
</div>
</div>
</div>
</div>
</div>
<div class="field is-horizontal">
<div class="field-label is-normal">
<label class="label">Fach</label>
</div>
<div class="field-body">
<div class="field">
<div class="control">
<div class="select">
<select bind:value="{newTask.subject}">
{#each subjects as subject}
<option>{subject}</option>
{/each}
</select>
</div>
</div>
</div>
</div>
</div>
<div class="field is-horizontal">
<div class="field-label is-normal">
<label class="label">Aufgabe</label>
</div>
<div class="field-body">
<div class="field">
<div class="control">
<input class="input" bind:value="{newTask.task}" type="text" placeholder="Hier Aufgabe eingeben...">
</div>
</div>
</div>
</div>
<div class="field is-horizontal">
<div class="field-label"></div>
<div class="field-body">
<div class="field is-grouped">
<div class="control">
<button type="submit" class="button is-success is-light">Hinzufügen</button>
</div>
<div class="control">
<button type="reset" class="button is-danger is-light">Zurücksetzen</button>
</div>
</div>
</div>
</div>
</form>
{/if}
{#each weekdays as weekday}
{#if weekdayTasks(weekday, tasks).length}
<h3>Meine Aufgaben für {weekday}</h3>
<table class="table is-striped">
<thead>
<tr>
<th>Status</th>
<th>Fach</th>
<th>Aufgabe</th>
</tr>
</thead>
<tbody>
{#each weekdayTasks(weekday, tasks) as task}
<tr>
<td>{task.status}</td>
<td><strong>{task.subject}</strong></td>
<td>{task.task}</td>
</tr>
{/each}
</tbody>
</table>
{/if}
{/each}
</div>
</main>
<footer class="footer">
  <div class="content has-text-centered">
    <p>______________________________________________________________</p>
    <p>
      <strong>Digitales Hausaufgabenheft</strong> by Philipp
    </p>
    <p>______________________________________________________________</p>
  </div>
</footer>

