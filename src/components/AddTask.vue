<template>
    <form @submit="onSubmit" class="add-form">
        <div class="form-control">
            <label for="text">Task</label>
            <input type="text" v-model="text" name="text" placeholder="Add Task">
        </div>
        <div class="form-control">
            <label for="day">Day</label>
            <input type="date" v-model="day" name="day" placeholder="Add Day">
        </div>
		<div class="form-control">
			<label for="time">Time</label>
			<input type="time" v-model="time" name ="time" placeholder="Add Time">
		</div>
        <!-- <div class="form-control">
            <label id="reminder-label">Set Reminder</label>
            <input id="reminder-box" type="checkbox" v-model="reminder" name="reminder">
        </div> -->
        <label id="reminder-label" for="reminder">Set Reminder</label>
        <input id="reminder-box" type="checkbox" v-model="reminder" name="reminder">

        <input type="submit" value="Save Task" class="btn btn-block">
    </form>
</template>

<script>
export default {
    name: "AddTask",
    data() {
        return {
            text: '',
            day: '',
			time: '',
            reminder: false
        }
    },
    methods: {
        onSubmit(e) {
            e.preventDefault();
            
            if(!this.text) {
                alert("Please add a task");
                return;
            }

            const timeWithFormat = this.onTimeChange(this.time);
            const newDate = new Date(this.day);
            const options = {
                weekday: 'long',
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            };
            const dateWithFormat = newDate.toLocaleDateString('en-US', options);

            const newTask = {
                id: Math.floor(Math.random() * 100000),
                text: this.text,
                day: dateWithFormat,
				time: timeWithFormat,
                reminder: this.reminder
            };

           this.$emit('add-task', newTask);

            this.text= "";
            this.day= "";
			this.time="";
            this.reminder= false;
        },
        onTimeChange(time) {
            let timeSplit = time.split(':'),
              hours,
              minutes,
              meridian;
            hours = timeSplit[0];
            minutes = timeSplit[1];
            if (hours > 12) {
              meridian = 'PM';
              hours -= 12;
            } else if (hours < 12) {
              meridian = 'AM';
              if (hours == 0) {
                hours = 12;
              }
            } else {
              meridian = 'PM';
            }
            const newTime = `${hours}:${minutes} ${meridian}`;
            return newTime;
        }
    }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
#reminder-label {
    display: inline-block;
}
#reminder-box {
    display: inline-block;
    max-width: 100px;
    margin-left: 1em;
    margin-bottom: 1em;
}
</style>
