<template>
  <div class="gstc-component" ref="gstc"></div>
</template>

<script>
import GSTC from 'gantt-schedule-timeline-calendar';
import 'gantt-schedule-timeline-calendar/dist/style.css';

let gstc, state;

// helper function
function generateItems(){
  const items = {};
  let start = GSTC.api.date().startOf('day').subtract(6,'day');
  for(let i =0;i<10;i++){
    const id = GSTC.api.GSTCID(i.toString());
    const rowId = GSTC.api.GSTCID(Math.ceil(Math.random()*4))
    start = start.add(1,'day');
    items[id] = {
      id,
      label:`Item ${i}`,
      rowId,
      time:{
        start: start.valueOf(),
        end: start.add(1,'day').endOf('day').valueOf()
      }
    }
  }
  return items;
}

export default {
  name: 'GSTC',
  mounted() {
    this.$refs.gstc.addEventListener('gstc-loaded', () => {
      // gstc is loaded and displayed
    });
    state = GSTC.api.stateFromConfig({
      licenseKey:'====BEGIN LICENSE KEY====\nXOfH/lnVASM6et4Co473t9jPIvhmQ/l0X3Ewog30VudX6GVkOB0n3oDx42NtADJ8HjYrhfXKSNu5EMRb5KzCLvMt/pu7xugjbvpyI1glE7Ha6E5VZwRpb4AC8T1KBF67FKAgaI7YFeOtPFROSCKrW5la38jbE5fo+q2N6wAfEti8la2ie6/7U2V+SdJPqkm/mLY/JBHdvDHoUduwe4zgqBUYLTNUgX6aKdlhpZPuHfj2SMeB/tcTJfH48rN1mgGkNkAT9ovROwI7ReLrdlHrHmJ1UwZZnAfxAC3ftIjgTEHsd/f+JrjW6t+kL6Ef1tT1eQ2DPFLJlhluTD91AsZMUg==||U2FsdGVkX1/SWWqU9YmxtM0T6Nm5mClKwqTaoF9wgZd9rNw2xs4hnY8Ilv8DZtFyNt92xym3eB6WA605N5llLm0D68EQtU9ci1rTEDopZ1ODzcqtTVSoFEloNPFSfW6LTIC9+2LSVBeeHXoLEQiLYHWihHu10Xll3KsH9iBObDACDm1PT7IV4uWvNpNeuKJc\npY3C5SG+3sHRX1aeMnHlKLhaIsOdw2IexjvMqocVpfRpX4wnsabNA0VJ3k95zUPS3vTtSegeDhwbl6j+/FZcGk9i+gAy6LuetlKuARjPYn2LH5Be3Ah+ggSBPlxf3JW9rtWNdUoFByHTcFlhzlU9HnpnBUrgcVMhCQ7SAjN9h2NMGmCr10Rn4OE0WtelNqYVig7KmENaPvFT+k2I0cYZ4KWwxxsQNKbjEAxJxrzK4HkaczCvyQbzj4Ppxx/0q+Cns44OeyWcwYD/vSaJm4Kptwpr+L4y5BoSO/WeqhSUQQ85nvOhtE0pSH/ZXYo3pqjPdQRfNm6NFeBl2lwTmZUEuw==\n====END LICENSE KEY====',
      list:{
        columns:{
          data:{
            [GSTC.api.GSTCID('id')] :{
              id:GSTC.api.GSTCID('id'),
              width:60,
              data:({row})=>GSTC.api.sourceID(row.id),
              header:{
                content:'ID'
              }
            },
            [GSTC.api.GSTCID('label')] :{
              id:GSTC.api.GSTCID('label'),
              width: 200,
              data:'label',
              header:{
                content: 'Label'
              }
            }
          }
        },
        rows:{
          [GSTC.api.GSTCID('1')]:{
            id:GSTC.api.GSTCID('1'),
            label:'Row 1'
          },
          [GSTC.api.GSTCID('2')]:{
            id:GSTC.api.GSTCID('2'),
            label:'Row 2'
          },
          [GSTC.api.GSTCID('3')]:{
            id:GSTC.api.GSTCID('3'),
            label:'Row 3'
          },
          [GSTC.api.GSTCID('4')]:{
            id:GSTC.api.GSTCID('4'),
            label:'Row 4'
          },
        }
      },
      chart:{
        items: generateItems()
      }
    });
    gstc = GSTC({
      element: this.$refs.gstc,
      state,
    });
    window.state = state;
    window.gstc = gstc;
  },
  beforeUnmount() {
    if (gstc) gstc.destroy();
  },
};
</script>
<style scoped>
.gstc-component {
  margin: 0;
  padding: 0;
}
</style>