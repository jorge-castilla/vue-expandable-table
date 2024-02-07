<script setup>
import { ref, onMounted, computed, watch } from 'vue'

// PROPS A DEFINIR:
const props = defineProps({
  customBorderColor: {
    type: String,
    default: '#1D3557'
  },
  thBackgroundColor: {
    type: String,
    default: '#A8DADC'
  },
  tdBackgroundColor: {
    type: String,
    default: '#F1FAEE'
  },
  expandableBackgroundColor: {
    type: String,
    default: '#fefae0'
  },
  borderWidth: {
    type: String,
    default: '1px'
  },
  tdPaddingY: {
    type: String,
    default: '12px'
  },
  tdPaddingX: {
    type: String,
    default: '12px'
  },
  thPaddingY: {
    type: String,
    default: '12px'
  },
  thPaddingX: {
    type: String,
    default: '12px'
  },
  expansiblePaddingX: {
    type: String,
    default: '12px'
  },
  expansiblePaddingY: {
    type: String,
    default: '12px'
  },
  data: {
    type: Array,
    default: () => null
  },
  columns: {
    type: Array,
    default: null
  },
  fullWidth: {
    type: Boolean,
    default: false
  }
})

const rows = ref([])

const updateRows = () => {
  // Extraer las claves de las columnas para saber qué excluir
  const columnKeys = props.columns.map((c) => c.field)

  rows.value = props.data.map((row) => {
    // Separar los datos que se van a mostrar directamente de los que irán en la expansión
    const displayData = {}
    const expandableData = {}
    let expandableDataCount = 0

    Object.entries(row).forEach(([key, value]) => {
      if (columnKeys.includes(key)) {
        // Si la clave está en columnKeys, va en displayData
        displayData[key] = value
      } else {
        // Si no, va en expandableData
        expandableData[key] = value
        expandableDataCount++
      }
    })

    return {
      ...displayData,
      isExpanded: false,
      expandableData, // Incluye todo lo que no está en 'columns'
      expandableDataCount
    }
  })
}

const expansiblePaddingYComputed = computed(() => {
  const charArray = props.expansiblePaddingY.split()
  let numberPortion = ''
  let stringPortion = ''
  charArray.forEach((char) => {
    if (typeof Number(char) === 'number') {
      numberPortion += char
    } else {
      stringPortion += char
    }
  })
  return numberPortion + stringPortion
})

watch(
  () => props.data,
  (newValue, oldValue) => {
    updateRows()
  }
)
watch(
  () => props.columns,
  (newValue, oldValue) => {
    updateRows()
  }
)

onMounted(() => {
  updateRows()
})

const baseHeight = 24
</script>

<template>
  <table v-if="data !== null && columns !== null" :class="fullWidth ? 'w-full' : ''">
    <thead>
      <th
        v-for="{ label, field } in columns"
        :key="field"
        class="custom-border-x custom-border-bottom custom-border-top"
      >
        {{ label }}
      </th>
    </thead>
    <template v-for="(row, index) in rows" :key="index">
      <tr @click="row.isExpanded = !row.isExpanded">
        <td v-for="{ field } in columns" :key="field" class="custom-border-x custom-border-bottom">
          {{ row[field] }}
        </td>
      </tr>
      <tr
        class="custom-transition-tr overflow-hidden custom-border-x"
        :class="row.isExpanded ? 'h-auto custom-border-bottom' : 'h-0'"
      >
        <td colspan="3" class="expansible-td">
          <div
            class="overflow-hidden flex flex-col justify-center expansible-child"
            :style="{
              height: row.isExpanded
                ? `calc(${baseHeight * row.expandableDataCount}px + ${expansiblePaddingYComputed})`
                : '0px',
              padding: `0px ${expansiblePaddingX}`
            }"
          >
            <div v-for="(value, key) in row.expandableData" :key="key">{{ key }}: {{ value }}</div>
          </div>
        </td>
      </tr>
    </template>
  </table>
</template>

<style scoped>
.custom-transition-tr{
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition: all 0.6s;

}
.expansible-td {
  border: none;
  vertical-align: center;
  padding: 0px !important;
}
.expansible-child {
  background-color: v-bind(expandableBackgroundColor);
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition: all 0.5s;
}
td {
  padding: v-bind(tdPaddingY) v-bind(tdPaddingX);
  background-color: v-bind(tdBackgroundColor);
}
th {
  padding: v-bind(thPaddingY) v-bind(thPaddingX);
  background-color: v-bind(thBackgroundColor);
}
.custom-border-x {
  border-left: v-bind(borderWidth) solid v-bind(customBorderColor);
  border-right: v-bind(borderWidth) solid v-bind(customBorderColor);
}
.custom-border-bottom {
  border-bottom: v-bind(borderWidth) solid v-bind(customBorderColor);
}
.custom-border-top {
  border-top: v-bind(borderWidth) solid v-bind(customBorderColor);
}
</style>
