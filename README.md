# BeeHive UI
This project was written with Vue 2 to handle Honeycombs in this "leveled" structure where each row can have N items and each honeycomb have it's own color.

## Usage
```
    import { BeeHive, BeeHiveRow, BeeHiveItem } from 'beehive-vue2';

    <BeeHive>
      <BeeHiveRow
        v-for="(career, index) in sampleData.levels"
        :index="index + 1"
        :children="career.roles.length"
        :key="index"
        :rowBefore="getRowBeforeChildren(index)"
        :label="career.id"
      >
        <BeeHiveItem
          v-for="role in career.roles"
          :key="role.id"
          :color="role.color"
          :item="{...role, level: career.id}"
          :active="role.id === selectedItem?.id"
          @select="selectHandler"
        >
          <p class="hexagon__title">
            {{role.name}}
          </p>
        </BeeHiveItem>
      </BeeHiveRow>
    </BeeHive>
```