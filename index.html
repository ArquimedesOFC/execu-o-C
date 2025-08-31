<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Visualizador de Execução C (Avançado)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.2/codemirror.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.2/theme/material-darker.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.2/codemirror.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.2/mode/clike/clike.min.js"></script>
    <style>
        body { font-family: 'Inter', sans-serif; overflow: hidden; }
        .CodeMirror { height: calc(100vh - 150px); font-size: 16px; border-radius: 0.5rem; }
        .highlight-line { background-color: rgba(100, 181, 246, 0.3) !important; }
        .variable-updated { animation: flash 0.7s ease-out; }
        @keyframes flash {
            0% { background-color: rgba(34, 197, 94, 0.4); }
            100% { background-color: transparent; }
        }
        .tab-button.active { border-bottom-color: #3b82f6; color: #3b82f6; }
        #output-view { white-space: pre-wrap; word-break: break-all; }
    </style>
</head>
<body class="bg-slate-100 text-slate-800">
    <div id="app" class="p-4 md:p-6 max-w-screen-2xl mx-auto">
        <header class="mb-4">
            <h1 class="text-3xl font-bold text-slate-900">Visualizador de Execução C</h1>
            <p class="text-slate-600">Escreva um código C e execute-o linha por linha para entender seu funcionamento.</p>
        </header>

        <div class="bg-white p-3 rounded-lg shadow-md mb-4 flex flex-wrap gap-3 items-center">
            <button id="run-btn" class="px-4 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 transition-colors shadow font-semibold">Analisar</button>
            <button id="next-btn" class="px-4 py-2 bg-green-600 text-white rounded-md hover:bg-green-700 transition-colors shadow font-semibold disabled:bg-slate-400 disabled:cursor-not-allowed" disabled>Próxima Linha (Enter)</button>
            <button id="reset-btn" class="px-4 py-2 bg-slate-600 text-white rounded-md hover:bg-slate-700 transition-colors shadow font-semibold">Resetar</button>
        </div>

        <main class="grid grid-cols-1 lg:grid-cols-2 gap-6" style="height: calc(100vh - 150px);">
            <div class="bg-white p-4 rounded-lg shadow-md h-full">
                <h2 class="text-xl font-semibold mb-2 text-slate-900">Editor de Código</h2>
                <textarea id="code-editor"></textarea>
            </div>

            <div class="flex flex-col gap-6 h-full">
                 <div class="bg-white p-4 rounded-lg shadow-md flex-shrink-0">
                    <div class="border-b border-slate-200">
                        <nav class="-mb-px flex space-x-6" aria-label="Tabs">
                            <button class="tab-button active" data-tab="variables">Variáveis (Stack)</button>
                            <button class="tab-button" data-tab="heap">Heap</button>
                            <button class="tab-button" data-tab="stack">Pilha</button>
                        </nav>
                    </div>

                    <div id="variables-tab" class="py-4 tab-content h-48 overflow-y-auto"></div>
                    <div id="heap-tab" class="py-4 tab-content hidden h-48 overflow-y-auto"></div>
                    <div id="stack-tab" class="py-4 tab-content hidden h-48 overflow-y-auto space-y-2"></div>
                </div>

                <div class="bg-white p-4 rounded-lg shadow-md flex-grow flex flex-col">
                    <h2 class="text-xl font-semibold text-slate-900">Saída do Programa</h2>
                    <pre id="output-view" class="bg-slate-900 text-white p-3 mt-2 rounded-md overflow-auto text-xs flex-grow"></pre>
                </div>
            </div>
        </main>
    </div>
    
    <div id="scanf-modal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center hidden z-50">
        <div class="bg-white p-6 rounded-lg shadow-xl w-full max-w-sm">
            <h3 class="text-lg font-bold mb-4">Entrada de Dados (scanf)</h3>
            <p id="scanf-prompt" class="mb-4 text-slate-600"></p>
            <input type="text" id="scanf-input" class="w-full border border-slate-300 rounded-md p-2 focus:ring-2 focus:ring-blue-500 focus:border-blue-500">
            <button id="scanf-submit" class="mt-4 w-full bg-blue-600 text-white py-2 rounded-md hover:bg-blue-700 transition-colors">Enviar</button>
        </div>
    </div>

    <script>
        const editorElement = document.getElementById('code-editor');
        const runBtn = document.getElementById('run-btn');
        const nextBtn = document.getElementById('next-btn');
        const resetBtn = document.getElementById('reset-btn');
        const variablesView = document.getElementById('variables-tab');
        const heapView = document.getElementById('heap-tab');
        const stackView = document.getElementById('stack-tab');
        const outputView = document.getElementById('output-view');
        const tabs = document.querySelectorAll('.tab-button');
        const tabContents = document.querySelectorAll('.tab-content');
        const scanfModal = document.getElementById('scanf-modal');
        const scanfPrompt = document.getElementById('scanf-prompt');
        const scanfInput = document.getElementById('scanf-input');
        const scanfSubmit = document.getElementById('scanf-submit');


        const initialCode = `// Cap08_ex10 - Troca de valores com ponteiros
#include <stdio.h>

void troca(int *a, int *b) {
    int temp;
    temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int x, y;
    printf("Digite o valor de x: ");
    scanf("%d", &x);
    printf("Digite o valor de y: ");
    scanf("%d", &y);
    
    printf("\\nAntes da troca:\\n");
    printf("x = %d, y = %d\\n", x, y);
    
    troca(&x, &y);
    
    printf("\\nDepois da troca:\\n");
    printf("x = %d, y = %d\\n", x, y);
    
    return 0;
}`;

        const editor = CodeMirror.fromTextArea(editorElement, {
            lineNumbers: true,
            mode: "text/x-csrc",
            theme: "material-darker",
            indentUnit: 4,
        });
        editor.setValue(initialCode);

        let executionState = {};

        function resetState() {
            executionState = {
                lines: [], allLines: [], functionMap: {}, structMap: {},
                currentLineIndex: -1,
                scopes: [{ id: 'scope_global', name: 'global', variables: {} }],
                callStack: [], heap: {}, heapCounter: 0, output: "",
                finished: true, lineMarkers: [], isWaitingForInput: false, scanfTarget: null,
                controlFlowStack: [],
            };
            nextBtn.disabled = true; runBtn.disabled = false;
            scanfModal.classList.add('hidden');
            if (editor.getDoc().getAllMarks().length > 0) { editor.getDoc().getAllMarks().forEach(mark => mark.clear()); }
            variablesView.innerHTML = '<p class="text-slate-500 text-sm">Clique em "Analisar" para começar.</p>';
            heapView.innerHTML = '<p class="text-slate-500 text-sm">Memória alocada (Heap) aparecerá aqui.</p>';
            stackView.innerHTML = '<p class="text-slate-500 text-sm">A pilha de chamadas (Stack) aparecerá aqui.</p>';
            outputView.textContent = '';
        }

        function findMatchingBrace(lines, startIndex) {
            let braceCount = 1;
            for (let i = startIndex + 1; i < lines.length; i++) {
                if (!lines[i] || typeof lines[i].text !== 'string') continue;
                for (const char of lines[i].text) {
                    if (char === '{') braceCount++;
                    else if (char === '}') braceCount--;
                }
                if (braceCount === 0) return i;
            }
            return -1;
        }

        function analyzeCode() {
            resetState();
            let code = editor.getValue().replace(/#include\s*<.*?>/g, '');
            executionState.allLines = code.split('\n').map((line, index) => ({ text: line, lineNumber: index }));
            executionState.lines = executionState.allLines.filter(line => line.text.trim() !== '' && !line.text.trim().startsWith('//'));

            const funcRegex = /(?:int|void|char|float|double|struct\s+\w+\*?)\s+([\w*]+)\s*\(([^)]*)\)\s*\{/g;
            let match;
            while((match = funcRegex.exec(code)) !== null) {
                 const name = match[1].replace('*', '');
                 const startLineNum = code.substring(0, match.index).split('\n').length - 1;
                 const startIndex = executionState.lines.findIndex(l => l.lineNumber >= startLineNum);
                 
                 const args = match[2].split(',').map(arg => {
                     const parts = arg.trim().split(/\s+/);
                     const varName = parts.pop().replace('*','');
                     return { name: varName, type: parts.join(' '), isPointer: arg.includes('*') };
                }).filter(a => a.name);
                executionState.functionMap[name] = { startLine: startLineNum, args };
            }

            if (!executionState.functionMap['main']) {
                executionState.output = "ERRO: Função 'main' não encontrada."; updateUI(); return;
            }
            prepareFunctionCall('main', []);
            executionState.finished = false; nextBtn.disabled = false; runBtn.disabled = true;
            updateUI();
        }

        function executeNextLine() {
            if (executionState.isWaitingForInput || executionState.finished) return;
            const lineInfo = executionState.lines[executionState.currentLineIndex];
            if (!lineInfo) { returnFromFunction(); }
            else {
                try { evaluateLine(lineInfo); }
                catch (e) {
                    console.error(e);
                    executionState.output += `\nERRO na linha ${lineInfo.lineNumber + 1}: ${e.message}\n`;
                    executionState.finished = true;
                }
            }
            if (!executionState.isWaitingForInput) { updateUI(); }
        }
        
        function getCurrentScope() {
            return executionState.scopes[executionState.scopes.length - 1];
        }

        function getVariable(name, scope = getCurrentScope()) {
            for (let i = executionState.scopes.length - 1; i >= 0; i--) {
                const s = executionState.scopes[i];
                if (s.variables[name]) {
                    return s.variables[name];
                }
            }
            return null;
        }

        function getVariableByAddress(address) {
             for (const scope of executionState.scopes) {
                for (const varName in scope.variables) {
                    if (scope.variables[varName].address === address) {
                        return scope.variables[varName];
                    }
                }
            }
            return null;
        }

        function evaluateExpression(expr) {
            expr = expr.trim();
            
            if (expr.startsWith('&')) {
                const varName = expr.substring(1);
                const variable = getVariable(varName);
                if (!variable.address) {
                    variable.address = `${getCurrentScope().id}_${varName}`;
                }
                return `"${variable.address}"`;
            }

            const funcCallRegex = /(\w+)\s*\(([^)]*)\)/g;
            expr = expr.replace(funcCallRegex, (match, funcName, argsStr) => {
                 const args = argsStr ? argsStr.split(',').map(arg => evaluateExpression(arg)) : [];
                 if (funcName === 'sqrt') return Math.sqrt(args[0]);
                 if (funcName === 'pow') return Math.pow(args[0], args[1]);
                 if (executionState.functionMap[funcName]) {
                     prepareFunctionCall(funcName, args, executionState.lines[executionState.currentLineIndex].lineNumber);
                     return 'FUNCTION_CALL_PENDING';
                 }
                 return match;
            });
            if (expr.includes('FUNCTION_CALL_PENDING')) return 'FUNCTION_CALL';

             const derefRegex = /\*(\w+)/g;
             expr = expr.replace(derefRegex, (match, varName) => {
                const pointer = getVariable(varName);
                if(pointer && pointer.isPointer && pointer.value !== 'NULL') {
                    const targetVar = getVariableByAddress(pointer.value);
                    if(targetVar) return targetVar.value;
                }
                return 0; // Dereferencing NULL or invalid pointer
             });
            
             const resolvedExpr = expr.replace(/[a-zA-Z_][\w]*/g, (name) => {
                 const variable = getVariable(name);
                 if (variable && variable.value !== undefined) {
                     if(variable.isPointer) return `"${variable.value}"`;
                     return variable.value;
                 }
                 return name;
            });

             try {
                return new Function(`return ${resolvedExpr}`)();
            } catch (e) {
                 return resolvedExpr;
            }
        }
        
        function evaluateLine(lineInfo) {
            let line = lineInfo.text.trim();
            if (line.endsWith(';')) line = line.slice(0, -1);
            
            const scope = getCurrentScope();
            let nextIndex = executionState.currentLineIndex + 1;

            const assignmentRegex = /^(.+?)\s*=\s*(.+)/;
            const declRegex = /^(int|float|char|double)\s+([\w,*\s\[\]=.]+)/;
            const printfRegex = /printf\("([^"]*)"(?:,\s*(.*))?\)/;
            const scanfRegex = /scanf\("([^"]+)"\s*,\s*&(\w+)/;
            const funcCallRegex = /^(\w+)\s*\((.*)\)/;
             const returnRegex = /^return\s*(.*)?/;

            let match;
            
            if ((match = line.match(scanfRegex))) {
                 executionState.isWaitingForInput = true;
                 executionState.scanfTarget = { name: match[2], format: match[1] };
                 scanfPrompt.textContent = `Entrada para ${match[1]} para '${match[2]}':`;
                 scanfModal.classList.remove('hidden');
                 scanfInput.focus();
                 return; 
            } else if ((match = line.match(printfRegex))) {
                 let formatStr = match[1];
                 let args = match[2] ? match[2].split(',').map(a => evaluateExpression(a.trim())) : [];
                 let argIndex = 0;
                 let output = formatStr.replace(/%(\.\d+)?f|%d|%s/g, (specifier) => {
                    const value = args[argIndex++];
                    if (specifier.includes('f')) {
                        const precisionMatch = specifier.match(/\.(\d+)/);
                        if (precisionMatch) { return parseFloat(value).toFixed(parseInt(precisionMatch[1])); }
                        return parseFloat(value);
                    }
                    return value;
                 }).replace(/\\n/g, '\n');
                 executionState.output += output;
            } else if((match = line.match(declRegex))) {
                 const type = match[1];
                 match[2].split(',').map(d => d.trim()).forEach(decl => {
                    const isPointer = decl.includes('*');
                    const varName = decl.replace('*', '').split('=')[0].trim();
                    let value = isPointer ? 'NULL' : (type === 'float' || type === 'double' ? 0.0 : 0);
                    if(decl.includes('=')) value = evaluateExpression(decl.split('=')[1].trim());
                    scope.variables[varName] = {type, value, isPointer, address: `${scope.id}_${varName}`};
                 });
            } else if ((match = line.match(funcCallRegex)) && executionState.functionMap[match[1]]) {
                if (evaluateExpression(line) === 'FUNCTION_CALL') return;
            } else if ((match = line.match(assignmentRegex))) {
                const lvalue = match[1];
                const rvalue = evaluateExpression(match[2]);
                if (rvalue === 'FUNCTION_CALL') return;

                if (lvalue.startsWith('*')) {
                    const ptrName = lvalue.substring(1);
                    const pointer = getVariable(ptrName);
                    const targetVar = getVariableByAddress(pointer.value);
                    if (targetVar) {
                        targetVar.value = rvalue;
                        targetVar.updated = true;
                    }
                } else {
                    const variable = getVariable(lvalue);
                    if (variable) {
                        variable.value = rvalue;
                        variable.updated = true;
                    }
                }
            } else if (line.match(returnRegex)) {
                returnFromFunction(); return;
            }
             executionState.currentLineIndex = nextIndex;
        }

        function prepareFunctionCall(funcName, argValues, returnLineNum) {
            const func = executionState.functionMap[funcName];
            executionState.callStack.push({ name: funcName, returnLineNum });
            const newScope = { id: `scope_${executionState.scopes.length}`, name: funcName, variables: {} };
            func.args.forEach((argDef, i) => {
                 newScope.variables[argDef.name] = { type: argDef.type, value: argValues[i], isPointer: argDef.isPointer };
            });
            executionState.scopes.push(newScope);
            executionState.currentLineIndex = executionState.lines.findIndex(l => l.lineNumber > func.startLine);
        }

        function returnFromFunction() {
            if (executionState.callStack.length <= 1) { executionState.finished = true; return; }
            const frame = executionState.callStack.pop();
            executionState.scopes.pop();
            executionState.currentLineIndex = executionState.lines.findIndex(l => l.lineNumber === frame.returnLineNum) + 1;
        }

        function handleScanfSubmit() {
            let value = scanfInput.value;
            const target = executionState.scanfTarget;
            if (target.format.includes('d')) value = parseInt(value, 10);
            else if (target.format.includes('f')) value = parseFloat(value);
            getVariable(target.name).value = value;
            
            scanfModal.classList.add('hidden');
            executionState.isWaitingForInput = false;
            executionState.currentLineIndex++;
            updateUI();
        }

        function updateUI() {
            if (executionState.finished) {
                nextBtn.disabled = true;
                 if(executionState.lineMarkers.length > 0) executionState.lineMarkers.pop().clear();
            }
             if (executionState.lineMarkers.length > 0) executionState.lineMarkers.pop().clear();
            if (!executionState.finished) {
                 const lineInfo = executionState.lines[executionState.currentLineIndex];
                 if (lineInfo) {
                    const marker = editor.getDoc().markText({ line: lineInfo.lineNumber, ch: 0 }, { line: lineInfo.lineNumber, ch: null }, { className: 'highlight-line' });
                    executionState.lineMarkers.push(marker);
                    editor.scrollIntoView({line: lineInfo.lineNumber, ch: 0}, 50);
                }
            }
            renderVariables(); renderHeap(); renderStack();
            outputView.textContent = executionState.output;
        }
        
        function renderVariables() {
            variablesView.innerHTML = '';
             executionState.scopes.forEach(scope => {
                const scopeDiv = document.createElement('div');
                scopeDiv.className = 'mb-4';
                scopeDiv.innerHTML = `<h3 class="font-bold text-sm uppercase text-slate-500">${scope.name} Scope</h3>`;
                const table = document.createElement('table');
                table.className = 'w-full text-sm mt-1';
                const tbody = document.createElement('tbody');
                Object.entries(scope.variables).forEach(([name, data]) => {
                    const row = document.createElement('tr');
                    row.className = `border-t ${data.updated ? 'variable-updated' : ''}`;
                    if(data.updated) data.updated = false;
                    
                    let displayValue = data.value;
                     if(data.isPointer) {
                         displayValue = `<span class="text-purple-400">${data.value}</span>`;
                     } else if (typeof displayValue === 'number' && !Number.isInteger(displayValue)) {
                        displayValue = displayValue.toFixed(2);
                     }

                    row.innerHTML = `<td class="py-1 pr-2 text-slate-600">${data.type}${data.isPointer ? '*' : ''}</td><td class="py-1 font-medium pr-2">${name}</td><td class="py-1 font-mono">${displayValue}</td>`;
                    tbody.appendChild(row);
                });
                table.appendChild(tbody);
                scopeDiv.appendChild(table);
                variablesView.appendChild(scopeDiv);
             });
        }

        function renderHeap() { /* ... heap rendering logic ... */ }
        function renderStack() { 
            stackView.innerHTML = '';
             if (executionState.callStack.length === 0) { 
                 stackView.innerHTML = '<p class="text-slate-500 text-sm">A pilha de chamadas está vazia.</p>';
                 return;
             }
             executionState.callStack.slice().reverse().forEach((frame, index) => {
                const div = document.createElement('div');
                div.className = `p-3 rounded-md text-sm ${index === 0 ? 'bg-sky-100 border border-sky-300 text-sky-800' : 'bg-slate-100 border border-slate-200 text-slate-600'}`;
                div.textContent = `Função: ${frame.name}`;
                stackView.appendChild(div);
            });
         }

        document.addEventListener('keydown', (event) => {
            if (event.key === 'Enter' && !executionState.isWaitingForInput && !nextBtn.disabled) {
                event.preventDefault();
                executeNextLine();
            }
        });
        scanfSubmit.addEventListener('click', handleScanfSubmit);
        scanfInput.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') handleScanfSubmit();
        });
        runBtn.addEventListener('click', analyzeCode);
        nextBtn.addEventListener('click', executeNextLine);
        resetBtn.addEventListener('click', () => {
             const currentCode = editor.getValue();
             resetState();
             editor.setValue(currentCode);
        });
        tabs.forEach(tab => {
            tab.addEventListener('click', () => {
                tabs.forEach(t => t.classList.remove('active'));
                tab.classList.add('active');
                tabContents.forEach(content => content.classList.add('hidden'));
                document.getElementById(`${tab.dataset.tab}-tab`).classList.remove('hidden');
            });
        });
        
        resetState();
    </script>
</body>
</html>

