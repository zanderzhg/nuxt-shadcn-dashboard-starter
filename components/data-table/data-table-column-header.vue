<script setup lang="ts">
import type { Column } from '@tanstack/vue-table';
import type { Task } from '~/pages/(dashboard)/tasks/data/schema';
import { cn } from '@/lib/utils';
import { ArrowDownIcon, ArrowUpIcon, CaretSortIcon, EyeNoneIcon } from '@radix-icons/vue';

interface DataTableColumnHeaderProps {
       column: Column<Task, any>;
       title: string;
}

defineProps<DataTableColumnHeaderProps>();
</script>

<script lang="ts">
export default {
       inheritAttrs: false,
};
</script>

<template>
       <div
              v-if="column.getCanSort()"
              :class="cn('flex items-center space-x-2', $attrs.class ?? '')"
       >
              <DropdownMenu>
                     <DropdownMenuTrigger as-child>
                            <Button
                                   variant="ghost"
                                   size="sm"
                                   class="h-8 -ml-3 data-[state=open]:bg-accent"
                            >
                                   <span>{{ title }}</span>
                                   <ArrowDownIcon
                                          v-if="column.getIsSorted() === 'desc'"
                                          class="ml-2 h-4 w-4"
                                   />
                                   <ArrowUpIcon
                                          v-else-if="column.getIsSorted() === 'asc'"
                                          class="ml-2 h-4 w-4"
                                   />
                                   <CaretSortIcon v-else class="ml-2 h-4 w-4" />
                            </Button>
                     </DropdownMenuTrigger>
                     <DropdownMenuContent align="start">
                            <DropdownMenuItem @click="column.toggleSorting(false)">
                                   <ArrowUpIcon class="mr-2 h-3.5 w-3.5 text-muted-foreground/70" />
                                   Asc
                            </DropdownMenuItem>
                            <DropdownMenuItem @click="column.toggleSorting(true)">
                                   <ArrowDownIcon
                                          name="i-radix-icons-arrow-down"
                                          class="mr-2 h-3.5 w-3.5 text-muted-foreground/70"
                                   />
                                   Desc
                            </DropdownMenuItem>
                            <DropdownMenuSeparator />
                            <DropdownMenuItem @click="column.toggleVisibility(false)">
                                   <EyeNoneIcon class="mr-2 h-3.5 w-3.5 text-muted-foreground/70" />
                                   Hide
                            </DropdownMenuItem>
                     </DropdownMenuContent>
              </DropdownMenu>
       </div>

       <div v-else :class="$attrs.class">
              {{ title }}
       </div>
</template>
