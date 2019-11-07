<template>
<div class='container'>
    <div class='todo'>
        <form class='todo__form' v-on:submit="submitForm">
            <input class='todo__input' type='text' v-model.trim="newTask" placeholder='please...enter anybody' v-on:keyup.enter='addTask' />
        </form>

        <div class='todo__content'>
            <ol class='todo__tasks'>
                <li v-for="(task, index) in tasks" v-bind:key="index">
                    {{task.name}}
                    <div v-on:click='removeTask(index)'>x</div>
                </li>
            </ol>
            <div class='todo__tasks-count'><span>Tasks length: {{tasks.length}}</span></div>
        </div>
    </div>
</div>
</template>

<script>
export default {
	name: 'app',
	data() {
		return {
			newTask: '',
			tasks: []
		};
	},
	methods: {
		submitForm(event) {
			let {
				newTask,
				tasks
			} = this;

			event.preventDefault();
			if (newTask) {
				const data = {
					id: tasks.length,
					name: newTask
				};
				tasks.push(data);
			}
			this.newTask = '';
		},

		removeTask(index) {
			const {
				tasks
			} = this;
			tasks.splice(index, 1);
		}

	}
};
</script>

<style lang="scss">
.container {
    max-width: 1200px;
    height: auto;
    min-height: 300px;
    background-color: #f7f7f7;
    margin: 80px auto;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
}

.todo {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    &__form {
        width: 60%;
    }

    &__content {
        width: 60%;
        margin: 0 auto;
    }

    &__input {
        width: 100%;
        padding: 10px 18px;
        margin: 30px 0 18px;
        font-size: 18px;

        &:focus {
            outline: none;
        }
    }

    &__tasks {
        display: flex;
        justify-content: flex-start;
        flex-direction: column;
        align-items: flex-start;

        li {
            display: flex;
            flex-direction: row;
            justify-content: space-between;
            width: 100%;
        }

        &-count,
        li {
            font-size: 18px;
        }

        &-count {
            display: flex;
            justify-content: flex-start;
            padding-bottom: 20px;
        }

    }
}
</style>
